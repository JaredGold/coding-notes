# Big O Notation

https://www.bigocheatsheet.com/

Big O notation is used in computer science to indicate the performance or complexity of an **algorithm**, *in a worst case scenario*

It typically describes the **number of execution steps**

It measures **the rate of growth of the time taken** with respect to the growth of the input data set size



## Common big O notation values

In order of complexity (from least to greatest):

| **Notation** | **Name**                        |
| ------------ | ------------------------------- |
| $O(1)$       | Constant                        |
| $O(log n)$   | logarithmic                     |
| $O(n)$       | linear                          |
| $O(n^2)$     | quadratic (or polynomial - n^n) |
| $O(2^n)$     | exponential                     |



Common will always take the same amount of time

Logarithmic will grow but near flatten out over time but never fully flatten.

Linear will always grow at the same rate. If you have 1 it goes at a speed of 1 but if you have 4 it goes at a speed of 4.

Quadratic grows drastically faster to a slower speed but may be better in the early stages

Exponential is stupidly slow



### Common algorithm's

Searching algorithm is a set of steps that are executed to find a value in a list of values

A counting algorithm is a set of steps to count the instances of one thing in a group of things

A sorting algorithm is a set of steps to put a list of things in a specified order (like smallest to largest)



## Examples

# O(1) constant

If an algorithm always takes the same number of steps to solve a problem, regardless of the input, it is said to be **constant**.

Example: A function that returns the first element of an array

```ruby
def first_elemet (arr)
    if ( !arr.nil? and arr.count > 0)
        arr[0]
    else
        nil
    end
end
```



# O (log n) - logarithmic

The divide and conquer search method (binary search or merge sort algorithm) is a well0known logarithmic algorithm. In this case, it is implied that "log n" is "log (opposite of ^) n".

Each time through the loop, the data set to search or sort is halved, so in the worst case, the algorithm will require log n steps (where n is the number of items in the input collection)



# O(n) - linear

A linear algorithm requires as many steps as there are values in the input data set in the worst case.

Example: A function that counts the occurrences of a value in an input data set.

```ruby
def count_val (arr,val)
    count = 0
    arr.each do |element|
        count += 1 if element == val
    end
    return count
end
```



# O(n^2) - quadratic (or polynomial)

In nested loops we find polynomial or quadratic algorithms. These execute some set of actions over the data set up to n times for an n-sized data set.

Example: A function that compares each value to each other value, such as bubble sort.

```ruby
def basic_sort(arr)
    done = false
    while (!done)
        done = true
        for i in 0..arr.length-1 do
            if arr[i] > arr[i+1]
                tmp=arr[i]
                arr[i]=arr[i+1]
                arr[i+1]= tmp
                done=false
            end
        end
    end
end
    
```


# O(2^n) Exponential

In recursive algorithms that call themselves multiple times, we may find exponential time. With exponential time, the time to execute doubles (or more) with each element in the input data set. One example is the recursive implementation of the Fibonacci sequence.

```ruby
def fibonacci(number)
    if (number <= 1) return number
        return fibonacci(number - 2) + fibonacci(number -1)
    end
end
```



# Calculating Big O

What is the complexity of this algorithm?

```ruby
let arr1 = [1,2,3,4]
let arr2 = [4,2,8,0]

# Search arr2 for each value in arr 1
let matching = []
arr1.each do |val1|
    arr2.each do |val2|
        if val1 == val2
            matching.push(val1)
            next
        end
    end
end
```

If n is the number of values in each array (4),

How many times will we go through the inner loop (worst case)? n(4)

How many times will we go through the other loop? n(4)

Overall, n*n or O(n^2)