# PATCH

## git format-patch



- **生成最近的1次commit的patch**  

`git format-patch HEAD^`

- **生成最近的2次commit的patch**  

`git format-patch HEAD^^`

- **生成最近的3次commit的patch**  

`git format-patch HEAD^^^`

- **生成最近的4次commit的patch**  

`git format-patch HEAD^^^^`

- **生成两个commit间的修改的patch**  

`git format-patch <r1>..<r2>`

> 包含两个commit. <r1>和<r2>都是具体的commit号

- **生成单个commit的patch**

`git format-patch -1 <r1>`

- **生成某commit以来的修改patch**

`git format-patch <r1>`

> 不包含该commit

- **生成从根到r1提交的所有patch**

`git format-patch --root <r1>`



## git am

- **查看patch的情况**

`git apply --stat 0001-limit-log-function.patch`

- **检查patch是否能够打上**

`git apply --check 0001-limit-log-function.patch`

> 如果没有任何输出，则说明无冲突，可以打上
>
> git apply是另外一种打patch的命令，其与git am的区别是，git apply并不会将commit message等打上去，打完patch后需要重新git add和git commit，而git am会直接将patch的所有信息打上去，而且不用重新git add和git commit,author也是patch的author而不是打patch的人

- **将名字为0001-limit-log-function.patch的patch打上**

`git am 0001-limit-log-function.patch`

`git am --signoff 0001-limit-log-function.patch`

> 添加-s或者--signoff，还可以把自己的名字添加为signed off by信息，作用是注明打patch的人是谁，因为有时打patch的人并不是patch的作者

- **将路径~/patch-set/*.patch 按照先后顺序打上**

`git am ~/patch-set/*.patch`

- **将已经在am过程中打上的patch废弃掉**

`git am --abort`

> am失败时，用以将已经在am过程中打上的patch废弃掉
>
> 比如有三个patch，打到第三个patch时有冲突，那么这条命令会把打上的前两个patch丢弃掉，返回没有打patch的状态

- **当git am失败，解决完冲突后，这条命令会接着打patch**

`git am --resolved`