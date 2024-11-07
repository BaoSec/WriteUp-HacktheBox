
Interface website:
![[Pasted image 20241107195624.png]]

Function and Feature:
- Login
- Signup

Objective:
- Get flag by login with `administrator`

-----
								STEP BY STEP GUIDE

1. Sign up account and login it
![[Pasted image 20241107195833.png]]
![[Pasted image 20241107195904.png]]

--> Check source code at `web_insomnia\Insomnia\app\Controllers\ProfileController.php`. So I see function index as below... it will get flag if request HTTP contain username = `administrator` and contain `JWT cookie` and display to screen.

--> Continue, I check `web_insomnia\Insomnia\app\Controllers\UserController.php`. So i also see function process login. There are one flaw logic code
![[Pasted image 20241107200429.png]]
condition in if clause contain flaw logic code such as:
- count ($json_data) return number of element in array JSON. If we fill out to 2 field `username` and `password` ==>  `count(json_data)` will return 2. BUT, `!` is being placed prior count (in PHP language, any value other than 0 will be negated to f`alse`, and 0 will be negated to `true`.)
==> condition if always return false ==> don't need fill out password, only fill out username is `administrator` and cookie server return.

2. Exploitation
Firstly, we need to create account have value `administrator`. if this account exist, get next step !
Open burpsuite, negative to `Repeater` tab to resend HTTP Request and resend account created before
![[Pasted image 20241107201905.png]]
then, we will delete password and set value again is administrator
![[Pasted image 20241107202257.png]]
Now, we have token of administrator. We use it to get flag below:
![[getflag.png]]


-----
Always double check your backend code because backend is the main cause of security vulnerabilities. !! In this case, the if conditional function in checking for misplaced array elements leads to vulnerability.

Thanks for reading.