``` markdown
# Queue in Java

Die Datenstruktur für eine Warteschlange wird durch das Interface `java.util.Queue` repräsentiert. Eine Queue funktioniert nach dem Prinzip "First In First Out" (FIFO), bei dem das zuerst eingefügte Element auch als erstes entnommen wird.

## Methoden des `java.util.Queue` Interfaces:

- `boolean add(E e)
- `boolean offer(E e)
- `E poll()
- `E remove()
- `E peek()
- `E element()


## Methoden des `java.util.Deque` Interfaces:

- `void addFirst(E e)
    
- `void addLast(E e)
- `boolean offerFirst(E e)
- `boolean offerLast(E e)
- `E pollFirst()
- `E pollLast()
- `E removeFirst()
- `E removeLast()
- `E peekFirst()
- `E peekLast()
- `E getFirst()
- `E getLast()
- `boolean removeFirstOccurrence(Object o)
- `boolean removeLastOccurrence(Object o)

Die `Deque` stellt auch Methoden für Queue- und Stack-Operationen bereit.

Diese kurze Dokumentation gibt einen Überblick über die grundlegenden Methoden der Queue und Deque in Java.