# multiple_login
Created with CodeSandbox

## Purpose
This application can choose different account type to login.
The string before "@" is defined as the user name.
And the user name cannot overlap with the consecutive six digits of the password.

For example:
```
username: abc12345
password: xxabc123wer
result: fail

username: abc12345
password: c12345er12fda
result: fail

username: abc12345
password: c124345ksfh
result: pass
```


## Vue Components
This page contain two vue component.
### AccountType
This component is used in render multiple account type.
use `v-for` to  render each order.
Add a new object of `accountTypeArr` in App.js to add a new type.

* Demo
![](https://i.imgur.com/TpR9yhM.png)



### InputBox
This component is used in render multiple input box.
use `v-for` to  render each order.
Add a new object of `inputArr` in App.js to add a new input box.

* Demo
![](https://i.imgur.com/jDwwKB7.png)

