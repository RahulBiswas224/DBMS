# Intuition
When I first looked at this problem, I thought, if I just collect all the same emails together in a pile and count them, any email that shows up more than once is a duplicate. It's kind of like sorting through a deck of cards to find your pairs!

# Approach
To solve this in SQL, I used the `GROUP BY` command to put all identical emails into their own separate groups. Once they are grouped, I need to check the size of each group. I used `COUNT(*)` to count how many rows are inside each email group. Finally, I used the `HAVING` clause to filter out the groups, only keeping the ones where the count is strictly greater than 1. 

*(Note: I remembered we have to use `HAVING` instead of `WHERE` here because we are filtering based on an aggregate function after the grouping happens!)*

# Complexity
- Time complexity:
We have to scan through the entire table and group the records. Depending on how the database engine does it (like using a hash table), it generally takes about $$O(n)$$ time, where $n$ is the number of rows in the `Person` table.

- Space complexity:
The database has to hold the grouped emails in its memory to count them. In the worst-case scenario where every single email is totally unique, it would take up $$O(n)$$ space.

# Code
```mysql []
# Write your MySQL query statement below
select email from Person group by email having count(*) > 1;
```