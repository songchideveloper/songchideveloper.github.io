```javascript
function ListNode(val) {
	this.val = val;
	this.next = null;
}

/**
* param {number[]} nums
* return {ListNode}
*/
function createLinkList(nums) {

	var head = new ListNode(nums[0]);
	var current = head;

	nums.forEach(function(n, i) {
		if (i > 0) {
			current.next = new ListNode(n);
			current = current.next;
		}
	})

	current.next = null;

	printLinkList(head);

	return head;

}

function printLinkList(head) {
	var output = []
	while(head.next != null) {
		output.push(head.val);
		head = head.next
	}
	output.push(head.val);
	console.log(output);
}
```
