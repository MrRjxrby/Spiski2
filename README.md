# Списки 2
# Задание 1
```
package com.mycompany.spiski21;

class Node {
    int data;
    Node prev;
    Node next;

    Node(int data) {
        this.data = data;
        this.prev = this;
        this.next = this;
    }
}

class DCLL {
    private Node head;

    public void add(int data) {
        Node newNode = new Node(data);

        if (head == null) {
            head = newNode;
        } else {
            Node tail = head.prev;
            tail.next = newNode;
            newNode.prev = tail;
            newNode.next = head;
            head.prev = newNode;
        }
    }

    public Node removeFirst() {
        if (head == null) {
            return null; 
        }

        Node removed = head;

        if (head.next == head) { 
            head = null;
        } else {
            Node tail = head.prev;
            head = head.next;
            head.prev = tail;
            tail.next = head;
        }

        removed.next = null;
        removed.prev = null;
        return removed;
    }

    public void insertOrdered(Node node) {
        if (node == null) return;

        if (head == null) { 
            head = node;
        } else if (node.data <= head.data) { 
            Node tail = head.prev;
            node.next = head;
            node.prev = tail;
            head.prev = node;
            tail.next = node;
            head = node; 
        } else { 
            Node current = head;

            while (current.next != head && current.next != null && current.next.data < node.data) {
                current = current.next;
            }

            Node nextNode = current.next;
            current.next = node;
            node.prev = current;

            if (nextNode != null) {
                node.next = nextNode;
                nextNode.prev = node;
            } else { // Если nextNode почему-то null (это не должно происходить)
                node.next = head;
                head.prev = node;
            }
        }
    }

    public void printList() {
        if (head == null) {
            System.out.println("Список пуст");
            return;
        }

        Node current = head;
        do {
            System.out.print(current.data + " ");
            current = current.next;
        } while (current != head);
        System.out.println();
    }
}

public class Spiski21 {
    public static void main(String[] args) {
        DCLL originalList = new DCLL();
        originalList.add(1);
        originalList.add(3);
        originalList.add(5);
        originalList.add(7);
        originalList.add(9);

        System.out.println("Perviy spisok:");
        originalList.printList();

        DCLL newList = new DCLL();
        Node removedNode;
        while ((removedNode = originalList.removeFirst()) != null) {
            newList.insertOrdered(removedNode);
        }

        System.out.println("Yporiadochenniy spisok:");
        newList.printList();
    }
}
```
# Задание 2:
```
package com.mycompany.spiski22;

class Node {
    int data;
    Node prev;
    Node next;

    Node(int data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

class DoublyLinkedList {
    private Node head;
    private Node tail;

    public void add(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            tail = newNode;
        } else {
            tail.next = newNode;
            newNode.prev = tail;
            tail = newNode;
        }
    }

    public Node removeMin() {
        if (head == null) {
            return null;
        }

        Node minNode = head;
        Node current = head;

        while (current != null) {
            if (current.data < minNode.data) {
                minNode = current;
            }
            current = current.next;
        }

        if (minNode == head) { 
            head = head.next;
            if (head != null) {
                head.prev = null;
            } else {
                tail = null; 
            }
        } else if (minNode == tail) { 
            tail = tail.prev;
            if (tail != null) {
                tail.next = null;
            }
        } else { 
            minNode.prev.next = minNode.next;
            minNode.next.prev = minNode.prev;
        }

        minNode.prev = null;
        minNode.next = null;

        return minNode;
    }

    public void addFirst(Node node) {
        if (node == null) return;

        if (head == null) { // Если новый список пуст
            head = node;
            tail = node;
        } else {
            node.next = head;
            head.prev = node;
            head = node;
        }
    }

    public void printList() {
        if (head == null) {
            System.out.println("Список пуст");
            return;
        }

        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }

    public boolean isEmpty() {
        return head == null;
    }
}

public class Spiski22 {
    public static void main(String[] args) {
        DoublyLinkedList originalList = new DoublyLinkedList();
        originalList.add(7);
        originalList.add(2);
        originalList.add(9);
        originalList.add(4);
        originalList.add(1);
        originalList.add(5);

        System.out.println("Spisok:");
        originalList.printList();

        DoublyLinkedList sortedList = new DoublyLinkedList();

        while (!originalList.isEmpty()) {
            Node minNode = originalList.removeMin();
            sortedList.addFirst(minNode);
        }

        System.out.println("Sorted Spisok:");
        sortedList.printList();
    }
}
```
# Задание 3:
```
package com.mycompany.spiski23;

class Node {
    int data;
    Node prev;
    Node next;

    Node(int data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

class DCLL {
    private Node head;

    public void add(int data) {
        Node newNode = new Node(data);
        if (head == null) { 
            head = newNode;
            head.next = head;
            head.prev = head;
        } else {
            Node tail = head.prev;
            tail.next = newNode;
            newNode.prev = tail;
            newNode.next = head;
            head.prev = newNode;
        }
    }

    public void bubbleSort() {
        if (head == null || head.next == head) {
            return; 
        }

        boolean swapped;
        do {
            swapped = false;
            Node current = head;

            do {
                Node nextNode = current.next;

                if (current.data > nextNode.data) {
                    int temp = current.data;
                    current.data = nextNode.data;
                    nextNode.data = temp;

                    swapped = true;
                }

                current = current.next;
            } while (current.next != head); 

        } while (swapped); 
    }

    public void printList() {
        if (head == null) {
            System.out.println("Список пуст");
            return;
        }

        Node current = head;
        do {
            System.out.print(current.data + " ");
            current = current.next;
        } while (current != head);

        System.out.println();
    }
}

public class Spiski23 {
    public static void main(String[] args) {
        DCLL list = new DCLL();

        list.add(7);
        list.add(3);
        list.add(9);
        list.add(2);
        list.add(6);

        System.out.println("Spisok::");
        list.printList();

        list.bubbleSort();

        System.out.println("Sorted Spisok:");
        list.printList();
    }
}
```
#Задание 4:
```
package com.mycompany.spiski24;
class Node {
    String data; 
    Node prev;
    Node next;

    Node(String data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

class DLL {
    private Node head;

    public void insertOrdered(String str) {
        Node newNode = new Node(str);

        if (head == null) {
            head = newNode;
            return;
        }

        Node current = head;

        while (current != null) {
            if (str.length() < current.data.length() || 
                (str.length() == current.data.length() && str.compareTo(current.data) < 0)) {
                newNode.next = current;
                newNode.prev = current.prev;

                if (current.prev != null) {
                    current.prev.next = newNode;
                } else {
                    head = newNode;
                }

                current.prev = newNode;
                return;
            }

            current = current.next;
        }

        Node tail = getTail();
        tail.next = newNode;
        newNode.prev = tail;
    }

    private Node getTail() {
        Node current = head;
        while (current.next != null) {
            current = current.next;
        }
        return current;
    }

    public void printList() {
        Node current = head;
        while (current != null) {
            System.out.println(current.data);
            current = current.next;
        }
    }
}

public class Spiski24 {
    public static void main(String[] args) {
        DLL list = new DLL();


        list.insertOrdered("apple");
        list.insertOrdered("pen");
        list.insertOrdered("car");
        list.insertOrdered("book");
        list.insertOrdered("bread");
        list.insertOrdered("milk");
        list.insertOrdered("juice");

        System.out.println("Spisok posle vstavki:");
        list.printList();
    }
}
```
