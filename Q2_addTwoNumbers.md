# 两数相加

[题目链接](https://leetcode-cn.com/problems/add-two-numbers/)

**思路**: 数字相加的思路，没什么特殊的


```python
def addTwoNumbers(l1: ListNode, l2: ListNode) -> ListNode:

      beginning_node = ListNode()
      tmp_node = beginning_node
      addition = 0

      while l1 and l2:
          add_sum = l1.val + l2.val + addition
          if add_sum >= 10:
              tmp_node.val = add_sum - 10
              addition = 1
          else:
              tmp_node.val = add_sum
              addition = 0

          l1 = l1.next
          l2 = l2.next

          if l1 and l2:
              tmp_node.next = ListNode()
              tmp_node = tmp_node.next
          else:
              remaining_node = l1 or l2

      while remaining_node:
          tmp_node.next = ListNode()
          tmp_node = tmp_node.next

          add_sum = remaining_node.val + addition
          if add_sum >= 10:
              tmp_node.val = add_sum - 10
              addition = 1
          else:
              tmp_node.val = add_sum
              addition = 0

          remaining_node = remaining_node.next

      if addition == 1:
          tmp_node.next = ListNode(1)

      return beginning_node
```

**之前的实现过程有一些可以提高的地方**，包括

1. 对于加法结果和进位符的计算过程实现的比较麻烦
2. 对于节点指针的使用比较粗糙：把最终返回结果从

     ```python
     beginning_node
     ```
     
     修改为
     
      ```python
     beginning_node.next
     ```
     
     可以简化节点指针的处理
     
**修改后的代码为**：


```python
def addTwoNumbers(l1: ListNode, l2: ListNode) -> ListNode:

      beginning_node = ListNode()
      tmp_node = beginning_node
      addition = 0
      
      # 当l1 l2全部被遍历完，且进位符不为1的情况下，停止遍历
      while l1 or l2 or addition:
          num1 = l1.val if l1 else 0
          num2 = l2.val if l2 else 0

          add_sum = num1 + num2 + addition
          tmp_node.next = ListNode(add_sum%10)
          addition = add_sum//10

          l1 = l1.next if l1 else None
          l2 = l2.next if l2 else None
          tmp_node = tmp_node.next

      return beginning_node.next
```
