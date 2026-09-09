 [Senior Design Project Info Page](https://github.com/codyfarlow1/Senior_Project_1)
-----------
# **GET REPO**
```
git clone https://github.com/b-rnie/Senior-Design-Project
git switch -c <branch-name>
```
-----------
# **BRANCH NAMING**

Branch name must be related to the work that is being done

--more info

EX: 
``` 
git switch -c pageFixing
```
-----------
# **PULL REQUEST PROCEDURES**


1. Make changes...

2. Apply [COMMIT MESSAGE FORMAT](#commit-message-format)
  
3. After pushing, create pull request: [Pull Request](https://github.com/b-rnie/Senior-Design-Project/compare)

<img width="1262" height="702" alt="image" src="https://github.com/user-attachments/assets/511a9155-3c1b-4e92-b7dc-0a3959cdee5a" />

4. Input changes made to files OR view changes.txt

5. QA / Reviewer looks and tests the code

6. Merge branch to main branch

-----------
# **CODE REVIEW REQUIREMENTS**

- At least one person separate from the pusher has to review the code before it can be merged to the main branch
- Ensure that the code is functional
- Ensure that all test cases are passed
- Add any comments on pull request, if applicable

--more requirements..


-----------
# **COMMIT MESSAGE FORMAT**
- Message should be short and contain detail of change

```
git add <name.file>
git commit -m "message"  
git push -u origin <branch-name>
```

OR

- Create txt/md file that lists the changes made
```
git add .
git commit -m "SEE changes.txt FILE"
git push -u origin <branch-name>
```
