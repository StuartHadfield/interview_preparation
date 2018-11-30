
These are first attempts. Some of them will be slow, and will not get full points.  This is mostly because of execution timeouts. Sad Stu, sad Ruby. Alas, time is limited

# Hash Tables: Ransom Note


```ruby
def check_magazine(magazine, note)
    letter_dict = magazine.each_with_object({}) do |letter, acc|
        acc.key?(letter) ? acc[letter] += 1 : acc[letter] = 1
    end

    can_create = true
    note.map do |letter|
        if letter_dict[letter].nil?
            can_create = false
            break
        else
            letter_dict[letter] -= 1
            if letter_dict[letter] < 0
                can_create = false
                break
            end
        end
    end

    print can_create ? "Yes" : "No"
end

check_magazine(['give', 'me', 'one', 'grand', 'today', 'night'],
['give', 'one', 'grand', 'today'])
```

    Yes

# Sherlock and Anagrams


```ruby
def sherlock_and_anagrams(s)
  str = s
  sorted_substrings = (1..str.size - 1).each_with_object([]) do |i, substrings|
      str.chars.each_cons(i) do |substring|
        substrings << substring.sort.join
      end
  end
  
  occurrences = sorted_substrings.each_with_object({}) do |substring, acc|
    acc[substring].nil? ? acc[substring] = 1 : acc[substring] += 1
  end
  
  occurrences.values.reduce(0) do |memo, val|
      memo += factorial(val) / (factorial(2) * factorial(val - 2))
  end
end

def factorial(n)
  (1..n).inject(:*) || 1
end

sherlock_and_anagrams('cdcd')
```




    5



# Count Triplets Geometric Progression


```ruby
def count_triplets(arr, factor)

  result_indices = []
  for i in (0..arr.size-1) do
    index_combos = [[i]]
    number = arr[i]
    2.times do
      number = number*factor
      valid_indices = arr.each_index.select { |j| arr[j] == number && j != i }
      index_combos << valid_indices
    end
    result_indices << index_combos if index_combos.flatten.compact.size > 2
  end

  combinations = result_indices.flat_map do |index_group|
    index_group[0].product(index_group[1], index_group[2])
  end

  combinations.reject! do |index_group|
    index_group.sort != index_group
  end
  combinations.size
end

factor = 1
arr = [1, 2, 1, 1, 2, 4]
count_triplets(arr, factor)

# In python this is really simple.

# def count_triplets(arr, r):
#     v2 = defaultdict(int)
#     v3 = defaultdict(int)
#     count = 0
#     for k in arr:
#         count += v3[k]
#         v3[k*r] += v2[k]
#         v2[k*r] += 1
#         print(v3)
#         print(v2)
#         print(count)

#     return count
```




    5


