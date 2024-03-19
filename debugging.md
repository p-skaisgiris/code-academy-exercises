# Debugging exercises

The following is a list of buggy python code snippets. Try debugging them using Pycharm's IDE debugger (click to make breakpoints, traverse the code using buttons or keyboard shortcuts (F7 for Step Into, F8 for Step Over in Pycharm) and become a detective to solve the mystery of the bug). Describe what is wrong and why in a comment and fix the code.

1. This code is supposed to compute an average of a list of numbers
```python
def calculate_average(numbers):
    total = 0
    for i in range(len(numbers)):
        total += i
    average = total / len(numbers)
    return average

numbers = [5, 10, 15, 20]
result = calculate_average(numbers)
print(result)
```

2. The following should return `True` if the input is 1 or 2
```python
def is_1_or_2(num):
    if num == 1 or 2:
        print('the number is 1 or 2')
        return True
    else:
        print('the number is not 1 or 2')
        return False

result = is_1_or_2(num=3)
print(result)
```

3. This code is supposed to compare the means of two lists where the second list is an extended list of the first one.

```python
def mean(lst):
    return sum(lst) / len(lst)


# Define the original set of values.
values = [8., 7., 9., 4., 6., 7., 8., 4.]

# Create a new list with the original values and add a few more
new_values = values
new_values.append(1.)
new_values.append(2.)
new_values.append(3.)
new_values.append(4.)
new_values.append(1.)

print(f"Difference in the mean: {mean(new_values) - mean(values)}")
```

4. This code attempts to concatenate a list of words into a sentence
```python
def create_sentence(words):
    sentence = ""
    for word in words:
        sentence = sentence + word + " "
    return sentence

word_list = ["The", "quick", "brown", "fox"]
result = create_sentence(word_list)
print(result)
```

5. This code should return a list of small elements (less than `threshold`) from the given list
```python
def filter_low(lst, threshold=5):
    for element in lst:
        low = []
        if element < threshold:
            low.append(element)
    return low
    
my_list = [5, 2, 12, 7, 3, 8]
result = filter_low(my_list)
print(result)
```

6. The following code should remove even numbers from a list
```python
def remove_even_numbers(numbers):
    for num in numbers:
        if num % 2 == 0:
            numbers.remove(num)
    return numbers

numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
result = remove_even_numbers(numbers)
print(result)
```

7. The following code is supposed to print the original and squared list of numbers
```python
def square_elements(numbers):
    for i in range(len(numbers)):
        numbers[i] = numbers[i] ** 2
    return numbers

numbers = [1, 2, 3, 4]
result = square_elements(numbers)
print(numbers)
print(result)
```

8. The parameter `weekday` is `True` if it is a weekday, and the parameter `vacation` is `True` if we are on vacation. We sleep in if it is not a weekday or we're on vacation. Return `True` if we sleep in. Exercise from [here](https://codingbat.com/prob/p173401).

```
sleep_in(False, False) → True
sleep_in(True, False) → False
sleep_in(False, True) → True
```

```python
def sleep_in(weekday, vacation):
    if vacation is True:
        return True
    elif weekday != True or vacation != True:
        return True
    else
        return False
        
result = sleep_in(False, False)
print(result)
```