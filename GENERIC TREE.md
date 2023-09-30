```python
class Generic_Tree:
    def __init__(self,data):
        self.data=data
        self.children=list()
```


```python
n1=Generic_Tree(5)
n2=Generic_Tree(2)
n3=Generic_Tree(9)
n4=Generic_Tree(8)
n5=Generic_Tree(7)
n6=Generic_Tree(15)
n7=Generic_Tree(1)

n1.children.append(n2)
n1.children.append(n3)
n1.children.append(n4)
n1.children.append(n5)

n3.children.append(n6)
n3.children.append(n7)
```

# PRINTING TREE RECURSIVELY 


```python
def print_generic_tree(root):
    if root==None:
        return 
    print(root.data)
    for child in root.children:
        print_generic_tree(child)
```


```python
print_generic_tree(n1)
```

    5
    2
    9
    15
    1
    8
    7
    

# PRINT GENERIC TREE WITH PARENT AND ITS CHILDRE 


```python
def print_generic_tree_2(root):
    if root==None:
        return 
    print(root.data,end=":")
    for child in root.children:
        print(child.data,end=",")
    print()
    for children in root.children:
        print_generic_tree_2(children)
```


```python
print_generic_tree_2(n1)
```

    5:2,9,8,7,
    2:
    9:15,1,
    15:
    1:
    8:
    7:
    

#### there is no base case that root is none but it is a edge case keep in mind becuase we itterate on list 

# TAKEINPUT ASKING FOR CHILDREN AND THEN TAKE 


```python
def takeinput():
    print("Enter the root")
    data=int(input())
    root=Generic_Tree(data)
    if data==-1:
        return None
    print("Enter the no of child :",root.data)
    c=int(input())
    for i in range(c):
        child=takeinput()
        root.children.append(child)
    return root
    
```


```python
root=takeinput()
print_generic_tree_2(root)
```

    Enter the root
    5
    Enter the no of child : 5
    4
    Enter the root
    2
    Enter the no of child : 2
    -1
    Enter the root
    3
    Enter the no of child : 3
    -1
    Enter the root
    4
    Enter the no of child : 4
    -1
    Enter the root
    6
    Enter the no of child : 6
    -1
    5:2,3,4,6,
    2:
    3:
    4:
    6:
    

# TAKING INPUT AS PREORDER CONFUSION 


```python
def take_input_pre():
    print("Enter the root")
    data=int(input())
    root=Generic_Tree(data)
    if data==-1:
        return None
    child=take_input_pre()
    root.children.append(child)
    return root
```

# NO OF NODES IN GENERIC TREE


```python
def num_nodes(root):
    if root==None:
        return 0
    count=1
    for child in root.children:
        count+=num_nodes(child)
    return count
    
```


```python
root=takeinput()
num_nodes(root)
```

    Enter the root
    5
    Enter the no of child : 5
    4
    Enter the root
    2
    Enter the no of child : 2
    -1
    Enter the root
    3
    Enter the no of child : 3
    -1
    Enter the root
    4
    Enter the no of child : 4
    -1
    Enter the root
    5
    Enter the no of child : 5
    -1
    




    5



# Sum of nodes data


```python
def sum_nodes(root):
    if len(root.children)==0:
        return root.data
    for child in root.children:
        sum=sum_nodes(child)
    return root.data+sum
```


```python
sum_nodes(root)
```




    10



# NODE WITH LARGEST DATA


```python
def largest_data(root):
    if root==None:
        return 
    maximum=root.data
    for child in root.children:
        c=largest_data(child)
        maximum=max(maximum,c)
    return maximum
```


```python
root=takeinput()
largest_data(root)
```

    Enter the root
    5
    Enter the no of child : 5
    4
    Enter the root
    2
    Enter the no of child : 2
    -1
    Enter the root
    3
    Enter the no of child : 3
    -1
    Enter the root
    4
    Enter the no of child : 4
    -1
    Enter the root
    5
    Enter the no of child : 5
    -1
    




    5



# HEIGHT OF GENERIC TREE


```python
def height(root):
    if root==None:
        return 0
    h=0
    for child in root.children:
        c=height(child)
        h=max(h,c)
    return h+1
```


```python
root=takeinput()
height(root)
```

    Enter the root
    5
    Enter the no of child : 5
    4
    Enter the root
    2
    Enter the no of child : 2
    -1
    Enter the root
    3
    Enter the no of child : 3
    -1
    Enter the root
    4
    Enter the no of child : 4
    -1
    Enter the root
    5
    Enter the no of child : 5
    -1
    




    2



# TAKEINPUT LEVELWISE


```python
import queue
def take_input_levelwise():
    q=queue.Queue()
    print("Enter the root :")
    data=int(input())
    root=Generic_Tree(data)
    q.put(root)
    if data==-1:
        return None
    while not(q.empty()):
        current_node=q.get()
        print("Enter the no of children ",current_node.data)
        childcount=int(input())
        for i in range(childcount):
            print("Enter the next child for ",current_node.data)
            child=int(input())
            child_node=Generic_Tree(child)
            current_node.children.append(child_node)
            q.put(child_node)
    return root
```


```python
root=take_input_levelwise()
print_generic_tree_2(root)
```

    Enter the root :
    5
    Enter the no of children  5
    4
    Enter the next child for  5
    2
    Enter the next child for  5
    -1
    Enter the next child for  5
    3
    Enter the next child for  5
    -1
    Enter the no of children  2
    4
    Enter the next child for  2
    -1
    Enter the next child for  2
    5
    Enter the next child for  2
    -1
    Enter the next child for  2
    -1
    Enter the no of children  -1
    -1
    Enter the no of children  3
    -1
    Enter the no of children  -1
    -1
    Enter the no of children  -1
    -1
    Enter the no of children  5
    -1
    Enter the no of children  -1
    -1
    Enter the no of children  -1
    -1
    5:2,-1,3,-1,
    2:-1,5,-1,-1,
    -1:
    5:
    -1:
    -1:
    -1:
    3:
    -1:
    

# PRINT TREE LEVELWISE


```python
def print_tree_levelwise(root):
    q=queue.Queue()
    q.put(root)
    while not(q.empty()):
        curr_node=q.get()
        print(curr_node.data,end=":")
        for child in curr_node.children:
            print(child.data,end=",")
            q.put(child)
        print()
    return 
```


```python
root=take_input_levelwise()
print_tree_levelwise(root)
```

    Enter the root :
    4
    Enter the no of children  4
    4
    Enter the next child for  4
    2
    Enter the next child for  4
    3
    Enter the next child for  4
    4
    Enter the next child for  4
    5
    Enter the no of children  2
    -1
    Enter the no of children  3
    -1
    Enter the no of children  4
    -1
    Enter the no of children  5
    -1
    4:2,3,4,5,
    2:
    3:
    4:
    5:
    

# X IS PRESENT OR NOT 


```python
def present(root,x):
    if root==None:
        return False
    if root.data==x:
        return True
    for child in root.children:
        mini_ans=present(child,x)
        if mini_ans==True:
            return mini_ans
    return False
```


```python
present(root,5)
```




    True



# NO OF LEAF NODE


```python
def leaf_count(root):
    if root==None:
        return 0
    count=0
    if len(root.children)==0:
        count+=1
    for child in root.children:
        count+=leaf_count(child)
    return count

```


```python
root=take_input_levelwise()
leaf_count(root)
```

    Enter the root :
    5
    Enter the no of children  5
    4
    Enter the next child for  5
    2
    Enter the next child for  5
    -1
    Enter the next child for  5
    3
    Enter the next child for  5
    -1
    Enter the no of children  2
    4
    Enter the next child for  2
    -1
    Enter the next child for  2
    5
    Enter the next child for  2
    -1
    Enter the next child for  2
    -1
    Enter the no of children  -1
    -1
    Enter the no of children  3
    -1
    Enter the no of children  -1
    -1
    Enter the no of children  -1
    -1
    Enter the no of children  5
    -1
    Enter the no of children  -1
    -1
    Enter the no of children  -1
    -1
    




    7



# NODE WITH MAXIMUM CHILD SUM 


```python
def sum_with_max_child(root):
    if root==None:
        return 0
    node=tree
    sum_1=tree.data
    for child in root.children:
        sum_1+=child.data
    for child in root.children:
        temp,sum_child=sum_with_max_child(child)
        if sum_child>sum_1:
            node,sum_1=temp,sum_child
    return node

        
```


```python
def replace_with_depth(root,d=0):
    if root==None:
        return 
    root.data=d
    for child in root.children:
        replace_with_depth(child,d+1)
```


```python
root=take_input_levelwise()
replace_with_depth(root)
print_tree_levelwise(root)
```

    Enter the root :
    5
    Enter the no of children  5
    4
    Enter the next child for  5
    1
    Enter the next child for  5
    2
    Enter the next child for  5
    3
    Enter the next child for  5
    4
    Enter the no of children  1
    -1
    Enter the no of children  2
    -1
    Enter the no of children  3
    -1
    Enter the no of children  4
    -1
    0:1,1,1,1,
    1:
    1:
    1:
    1:
    

# STRUCTURE IDENTICAL 


```python
def isIdentical(tree1, tree2):
    if tree1==None and tree2==None:
        return True
    l1=len(tree1.children)-1
    l2=len(tree2.children)-1
    if l1!=l2:
        return False
    if tree1.data!=tree2.data:
        return False
    while l1>=0 and l2>=0:
        result=isIdentical(tree1.children[l1],tree2.children[l2])
        if result==False:
            return result
        l1-=1
        l2-=1
    return True
```


```python
root1,root2=take_input_levelwise(),take_input_levelwise()
isIdentical(root1,root2)
if isIdentical==False:
    print("false")
else:
    print("True")

```

    Enter the root :
    5
    Enter the no of children  5
    4
    Enter the next child for  5
    1
    Enter the next child for  5
    2
    Enter the next child for  5
    3
    Enter the next child for  5
    4
    Enter the no of children  1
    -1
    Enter the no of children  2
    -1
    Enter the no of children  3
    -1
    Enter the no of children  4
    -1
    Enter the root :
    5
    Enter the no of children  5
    3
    Enter the next child for  5
    1
    Enter the next child for  5
    2
    Enter the next child for  5
    3
    Enter the no of children  1
    -1
    Enter the no of children  2
    -1
    Enter the no of children  3
    -1
    True
    

# NEXT LARGER


```python
def larger_next(root,n,l=[]):
    if root==None:
        return l
    if root.data>n:
        l.append(root.data)
    for child in root.children:
        larger_next(child,n,l)
    return l
```


```python
root=take_input_levelwise()
l=larger_next(root,10)
l.sort()
print(l[0])
```

    Enter the root :
    5
    Enter the no of children  5
    4
    Enter the next child for  5
    11
    Enter the next child for  5
    12
    Enter the next child for  5
    4
    Enter the next child for  5
    3
    Enter the no of children  11
    0
    Enter the no of children  12
    0
    Enter the no of children  4
    0
    Enter the no of children  3
    0
    11
    


```python

```
