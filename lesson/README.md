# ![Computer Science - Stacks and Queues - Setup](./assets/hero.png)

## Setting the Stage

TKTK VIDEO

Stacks and queues in computer science are a lot like stacks and queues in real life. It helps if you think of stacks of pancakes and queues (lines) of people.

Let’s take a look.

It’s Saturday morning, and out of the kindness of your heart, you decide to make pancakes for your family. You’re gathering all the ingredients when you check the fridge and discover - you’re out of eggs! You rush to the grocery store, grab the eggs… and of course the line to check out (the queue) is 5 people deep. You move to the back and wait your turn.

Waiting in line for the cash register mirrors how a queue works in computer science. They’re defined by first in, first out behavior. That is, the first thing that’s added to a queue will be the first thing removed; the first person in line will be the first person who gets to check out.

Now for stacks. You’ve made it home and the pancakes are coming together beautifully. As you cook, you flip the pancakes off the griddle and onto a plate. You finish up the last batch and bring your pancakes to the table to serve your family.

Which pancakes are going to be taken first? The hot, fresh pancakes on the top of the stack? Or the pancake on the bottom that’s now cold and getting smushed? We know which one we’d take--the hot one on the top.

Watching your family take the fresh pancakes off the top of the plate is how a stack works. A stack is defined by last in, first out behavior--the opposite of how a queue works. The last thing added to the stack - the freshest pancake - is the first thing to be removed.

## Visualizing Stacks and Queues

Stacks and queues are defined by their behavior - in other words, how items are added to and removed from them.

- Stacks operate on “last in, first out” behavior. The last, most recently added item, is first to be removed.
- Queues, on the other hand, operate on “first in, first out” behavior. Items are removed in the order they were added, from first to last.

<br>

<img src="./assets/stacks-queues-1.png" alt="stack vs queue order">

## Stacks in Programming

Obviously, stacking (and eating) pancakes is more delicious and a lot less complicated than computer science. But, stacks and queues are behind a lot of the computer functionalities you know and love.

Have you ever used the “back” button on your browser? Used the “undo” or Cmd-Z function? You interacted with a stack! All of these examples refer to the most recent action — hence, “last in, first out” (LIFO).

The function call stack is another common example of stacks in programming. When you call a function to execute, it’s pushed to the top of the stack and runs until we add another function to the stack, which then runs until it returns (or another function is pushed on top). You can keep adding functions until you’ve run out of space in the stack - in which case, you’ve reached stack overflow.

(If only you could have pancake stack overflow!)

![Website Page](./assets/clicking-back-button.png)

## Queues in Programming

Queues also have applications you’re probably pretty familiar with.

Have you ever sent a document to the printer? Documents in the queue will print in the order they were sent, from first to last. That’s where we get “first in, first out,” or FIFO.

Computer processing unit (CPU) scheduling is also based on a queue. Tasks are executed in the order in which they were called, while execution of tasks further down in the queue is put on hold until resources are available.

<img src="./assets/stacks-queues-2.png" alt="printer queue">

## Different, But the Same

Stacks and queues might seem totally different, but they actually have a lot in common. They can both be implemented as an array or as a linked list, and we can perform **the same relatively limited set of actions on them**.

The tradeoff for limited functionality? Great runtimes, which are the same for stacks and queues! Check it out:

| Function    | Name in a stack | Name in a queue | Complexity |
| ----------- | --------------- | --------------- | ---------- |
| Access      | `Peek`          | `Peek`          | `O(1)`     |
| Insert      | `Push`          | `Enqueue`       | `O(1)`     |
| Delete      | `Pop`           | `Dequeue `      | `O(1)`     |
| Check empty | `IsEmpty`       | `IsEmpty`       | `O(1)`     |


The other thing that stacks and queues have in common is that they can both be implemented as an **array** or as a **linked list**.

Other than using different underlying data structures, there’s no major difference between array and linked list implementation. Which you use depends on how your data is already structured and how you expect to be inserting or removing elements. In the next section, we’ll look at each implementation for each data structure.

## Implementing Stacks

### Linked List Implementation

```js
class Node {
  constructor(data, next = null) {
    this.data = data;
    this.next = next;
  }
}

class Stack {
  constructor() {
    this.head = null;
  }

  push(data) {
    this.head = new Node(data, this.head);
  }

  pop() {
    let data = this.head.data;
    this.head = this.head.next;
    return data;
  }

  peek() {
    return this.head.data;
  }

  isEmpty() {
    return this.head == null;
  }
}
```

### Array Implementation

```js
class Stack {
  constructor() {
    this.items = [];
  }

  push(item) {
    this.items.push(item);
  }

  pop() {
    return this.items.pop();
  }

  peek() {
    return this.items[this.items.length - 1];
  }

  isEmpty() {
    return this.items.length === 0;
  }
}
```

## Implementing Queues

### Linked List Implementation

```js
class Node {
  constructor(data, next = null, prev = null) {
    this.data = data;
    this.next = next;
    this.prev = prev;
  }
}

class Queue {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  enqueue(data) {
    let newNode = new Node(data, null, this.head);

    if (!this.head) {
      this.head = newNode;
    } else {
      this.tail.next = newNode;
      newNode.prev = this.tail;
    }

    this.tail = newNode;
  }

  dequeue() {
    let data = this.head.data;
    this.head = this.head.next;
    return data;
  }

  peek() {
    return isEmpty() ? 'empty list!' : this.head.data;
  }

  isEmpty() {
    return this.head == null;
  }
}
```

### Array Implementation

```js
class Queue {
  constructor() {
    this.items = [];
  }

  enqueue(data) {
    this.items.push(data);
  }

  dequeue() {
    return this.items.shift();
  }

  peek() {
    return isEmpty() ? 'empty list!' : this.items[0];
  }

  isEmpty() {
    return this.items.length === 0;
  }
}
```

## Variations on the Queue: Priority queue

Queues have a couple of unique implementations we’ll touch on quickly.

The first is a **priority queue**. They have three rules in addition to the typical rules of a queue:

1. Every item has a priority associated with it.
2. An element with high priority is dequeued before an element with low priority.
3. If two elements have the same priority, they are served according to their order in the queue.

Have you ever been waiting in an airport security line in the U.S., only to be passed by someone with TSA Pre-Check? They still wait in line, but their “priority” moves them up more quickly.

CPU scheduling is commonly implemented as a priority queue. While the first tasks are completed first, any task that’s a “priority” will be moved up.

<img src="./assets/stacks-queues-3.png" alt="airline security line as a priority queue">

## Variations on the Queue: Double-Ended Queues

A double-ended queue (“deque,” for short) is a queue that performs insertions and deletions at both ends. It’s typically implemented with a doubly linked list or a dynamic array. These are often used for task-scheduling algorithms.

Have you ever been dead last in a long line at the grocery store only to see a cashier one lane over open up their register? Typically, that cashier will beckon to you to jump into their lane so you can be checked out right away. That’s basically what happens in a deque.

In computer science, this might be comparable to spreading tasks between several different servers as equally as possible. Each of these server machines maintains a double-ended queue of tasks that they need to crunch through. Mostly, this deque just functions as a regular queue, adding tasks to the end and processing them in the order they were received (FIFO). However, if one of your servers has no tasks in its own queue, it can take from the end of another server’s queue. They help each other out!

<img src="./assets/stacks-queues-4.png" alt="shopping checkout line as a double ended queue">


## Let’s Talk About Interviews

If stacks or queues come up in an interview, you’ll likely be asked to perform operations such as sorting, inserting, and finding values — and it only gets more complicated from there.

- [This article](https://www.geeksforgeeks.org/stack-data-structure/) on stacks outlines some standard problems that could come up in interviews.
- The [same article](https://www.geeksforgeeks.org/queue-data-structure/), but for queues.
- Don’t forget to review [priority queues](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/) and [deques](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/). (You might not be asked to build one of these, mostly to explain how they work and their uses.)

Use these visualization tools to practice building stacks and queues:

- Stacks: [array implementation](https://www.cs.usfca.edu/~galles/visualization/StackArray.html) and [linked list implementation](https://www.cs.usfca.edu/~galles/visualization/StackLL.html).
- Queues: [array implementation](https://www.cs.usfca.edu/~galles/visualization/QueueArray.html) and [linked list implementation](https://www.cs.usfca.edu/~galles/visualization/QueueLL.html).

<br>

![Brain](./assets/interviews.png)