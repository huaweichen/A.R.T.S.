---
layout: default
title:  "Add Two Numbers"
permalink: add-two-numbers.html
---

### Problem

##### [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

### Solution

##### [Solution Link](https://leetcode.com/submissions/detail/236313588/)

```PHP
<?php

class ListNode
{
    public $val = 0;
    public $next = null;

    function __construct($val)
    {
        $this->val = $val;
    }
}


class Solution
{
    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function addTwoNumbers($l1, $l2)
    {
        $carry = 0;
        $output = new ListNode(0);
        $tmp = $output;

        while (!is_null($l1->val) || !is_null($l2->val)) {
            $l1Node = $l1->val ?? 0;
            $l2Node = $l2->val ?? 0;

            $sum = $l1Node + $l2Node + $carry;

            $tmp->next = new ListNode($sum % 10);
            $carry = floor($sum / 10);

            $l1 = $l1->next;
            $l2 = $l2->next;
            $tmp = $tmp->next;
        }

        if ($carry > 0) {
            $tmp->next = new ListNode(1);
        }

        // $n1 = new ListNode(7);
        // $n1->next = new ListNode(0);
        // $n1->next->next = new ListNode(8);
        return $output->next;
    }
}

$l1 = new ListNode(2);
$l1->next = new ListNode(4);
$l1->next->next = new ListNode(3);


$l2 = new ListNode(5);
$l2->next = new ListNode(6);
$l2->next->next = new ListNode(4);

$solution = new Solution();
$result = $solution->addTwoNumbers($l1, $l2);

```