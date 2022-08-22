+++
date = "2022-08-22"
title = "File Permission"
description = "Use `chmod` to change file permission "
slug = ""
authors = ["Shane"]
tags = ["Linux"]
categories = ["Dev","Linux"]
externalLink = ""
series = ["Dive into Linux sys"]
+++
## Types of uesers
* There are 3 types of uesers in Linux sys:
  * User:The owner of the file.
  * Group:A user-group can contain multiple users. All users belonging to a group will have the same Linux group permissions access to the file. 
  * Other: Any one else
## Types of permission
* 3 tpyes of File Permissions
  * read(r,4), write(w,2), execute(x,2)
  * -rwx-rwx-rwx:the permission of User, Group and Other
## How to change permission
  * Use `chomd` to change the permission
  * cacluate the point of each permission of the owner
  * Use digital number to change the permission
    * `chmod 741 some-file`
      * 7:r+w+x=4+2+1=7
      * 4:-+w+-=0+4+0=4
      * 1:-+-+x=0+0+1=1
  * Use characters to change the permission
    * User Denotations:
        | alias | group |
        | ----- | ----- |
        |   u   | user/owner|
        |   g   | group |
        |   o   | other |
        |   a   |  all  |
    * `chmod o=rwx some-file`
      * give the permission of rwx to other 
    * `chmod u-r some-file`
      * remove read permission for user
  * change the group
    * `sudo chmod group-name some-file`
## Reference
>  https://www.guru99.com/file-permissions.html#:~:text=Linux%20divides%20the%20file%20permissions,ownership%20of%20a%20file%2Fdirectory.



