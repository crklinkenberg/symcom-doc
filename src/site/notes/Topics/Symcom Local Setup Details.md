---
{"dg-publish":true,"permalink":"/topics/symcom-local-setup-details/"}
---

# Prerequisites

 + **Windows Operating System**
 + **XAMPP 7.1.33**
 + **PHP Ver. 7.1 - 7.2**
 + **Composer 1.6.3**

     ```diff
     - THE FOLLOWING CHANGES WILL NOT AFFECT THE EXISTING SETUP OR CONFIGURATION OF THE SYSTEM -
     ```

1. Get the Exact **```Xampp7.1.3 from the given link.```** [Xampp7.1.3](https://udomain.dl.sourceforge.net/project/xampp/XAMPP%20Windows/7.1.33/xampp-windows-x64-7.1.33-1-VC14-installer.exe).
   - When installing Xammp Follow the Installation normally and Install **Xampp to new folder** if there's Xampp already installed.<br />
     **Example:** ```C:/xampp2```
   - If there's no Xampp installed previously in your system then the default path will be
     **Example:** ```C:/xampp```
     <br /><br />
 2. **Next,** **Open Powershell with Administrator privilege:** and then run command: <!-- ```Set-ExecutionPolicy RemoteSigned``` -->

```

Set-ExecutionPolicy RemoteSigned
```
**NOTE** 
> This will enable us to run the scripts.
3. And then navigate to the **```Xampp htdocs```** location and clone the repository or place/paste your downloaded project here.  
   - **Example:** ```C:/xampp/htdocs```
   <br /><br />
   - Skip the below command ```git clone https://github.com/crklinkenberg/symcom01Production.git``` if you are using downloaded project.
   <br /><br />
   ```
   git clone https://github.com/crklinkenberg/symcom01Production.git
   ```
   - Now our project location is this ```C:/xampp/htdocs/symcom01Production``` here **symcom01Production** is the project folder name. 
   
<!-- -[x] Then run, ```.\Script01.ps1```. This script will install Xampp, Git, and Download Composer. **1.6.3**. -->
- [x] Next, use the script which will Download Composer **1.6.3** in your system.<br /><br />
   - Open Elevated administrator ```Powershell``` and navigate to the location.<br /><br />
   ```
   C:/xampp/htdocs/symcom01Production/scripts
   ```
   - Then run the following command.<br /><br />
   ```
   .\Script01.ps1
   ```
   
**NOTE** 
> Running the ```Script01.ps1``` will asks for the location of the **Xampp directory** ```which is```.<br /><br />
   ```
   C:/xampp/
   ```
> Then the script will complete the ```composer install``` command and will complete the process.
<br /><br />**Composer** wil be saved into a new folder at.<br />
     **```C:\NeededFiles```**<br /><br />
```diff
- DO NOT DELETE THE FOLDER -
```
<br />

4. Now get your database databse file ready with you in this case "production stage database file" (i.e. xxxxxxxxxxx.sql) form AWS S3(if you have the access to it). Or have your .sql file ready with you that is provide to you.<br /><br />

- Now, Let’s start  our xampp server.
- Go to the below mentioned folder and right click on the xampp-control.exe and then click on Run as Administrator. This will open the Xampp control panel window.
- **Example** ```C:/xampp/xampp-control.exe```
- Now Xampp control panel window is open.
- Now Click on start button for both Apache and MySQL and wait until they turn green and then after that folow the instructions below.
- After starting the local Xampp Server, Go to ```http://localhost/phpmyadmin/``` in your web browser.
- Now, Create a database in ```http://localhost/phpmyadmin/``` with any name
- **Example** ```my_database```
- Now, to import the database, we will used specified tools of xampp (i.e. Using terminal and mysql command)
- To open the terminal. Find or open the Xampp control panel window first (which is mentioned above).
- Now, find a button named **Shell** in the right hand side of the Xampp control panel window and click that button and then use the following command in the terminal:
- ```mysql -u root -p my_database < "location of the .sql file"```
- Here in the above command

  ```
  root : is database username
  -p : stands for password which is blank by default
  my_database : is the database which we created in the http://localhost/phpmyadmin/
  "location of the .sql file" : should be the path of the .sql file that you have with you to import
  ```
- **Example in my case** ```mysql -u root -p my_database < "C:/Users/Mypc/Downloads/production_repertory.sql"```
- After successfully processing the above command our downloaded databse .sql file will git imported into our ```http://localhost/phpmyadmin/``` database which we created in above step.(Which is in my case "my_database")   

<!--

```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ dfgdfgdfgd@@
```
-->






# Installation


1. Go to your project directory which is in my case ```C:/xampp/htdocs/symcom01Production```, delete the existing **.htaccess** file and then rename **.htaccess-local** to **.htaccess**.

2. Change the configuration in the mentioned location: **```config/route.php```**
   - Open this file with an editor and change the database configuration with your details: <br /><br />

		```
		$dbUsername = 'root'; // The default Xampp database username is root.
		$dbPassword = ''; // The dufault Xampp database pasword is blank.
		$dbName = 'my_database'; // In my case the databse name is my_database, which we created in the above mentioned steps. 
		```
   - In this file change ```$absoluteUrl``` variable value to your application URL. In current example my application URL is ```http://localhost/symcom01Production/```
   - Chage
		```
   		$absoluteUrl = (isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] === 'on' ? "https" : "http") . "://$_SERVER[HTTP_HOST]/";
   		```
   - To
     
     		
     		$absoluteUrl = "http://localhost/symcom01Production/";
     		
     
3. Now inside **C:/xampp/htdocs/symcom01Production/dev-exp** directory delete the existing **check-if-comparison-table-exist.php** page and then rename **check-if-comparison-table-exist-local.php** page to **check-if-comparison-table-exist.php**

4. Follow the steps below for the location: ```C:/xampp/htdocs/symcom01Production/symcom/api```
   - Delete the existing .env file and then rename .env.development to .env on current location.
   - Now Open this .env file with an editor and change the database details as we have done in above mentioned steps. For me the database details are:

		```
		DB_DATABASE=my_database
		DB_USERNAME=root
		DB_PASSWORD=
		```
5. Open file ```constants.php``` in an editor, go to the location: ```C:/xampp/htdocs/symcom01Production/symcom/api/config/constants.php```
   - Here in this file change developemt environment's ```api_base_path``` url value to your application url value. Which is in my case ```http://localhost/symcom01Production/symcom/api/public/```
   
		Change
		```
   		if (app()->environment('development')) {
			$configArray2 ['api_base_path'] = 'http://dev.reference-repertory.com/symcom/api/public/';  
		}
		```
   		To
   		```
     		if (app()->environment('development')) {
			$configArray2 ['api_base_path'] = 'http://localhost/symcom01Production/symcom/api/public/';  
		}
   		```
6. After completing the above steps, the application setup is done. You can now open the application in a we browser using the application URL
      ```
      http://localhost/symcom01Production/
      ```
        
<!--   - Now in on your cmd or terminal at this location and run below command
		```
		php artisan key:generate
		```
	
5. To fulfill some of our custom requirements we need to do the following changes:
	
   - Location: ```project-folder-name/symcom/api/vendor/laravel/passport/src/Bridge/UserRepository.php``` Here in this script(UserRepository.php) we have to add the below mentioned function at the end inside the class. Just copy the below function and paste /add it in UserRepository.php
		```
	
		/**
		 * Custom added
		 */
		public function getEntityByUserCredentials($username, $password, $grantType, ClientEntityInterface $clientEntity, $provider)
		{
			$provider = config('auth.guards.'.$provider.'.provider');

			if (is_null($model = config('auth.providers.'.$provider.'.model'))) {
				throw new RuntimeException('Unable to determine authentication model from configuration.');
			}

			if (method_exists($model, 'findForPassport')) {
				$user = (new $model)->findForPassport($username);
			} else {
				$user = (new $model)->where('email', $username)->first();
			}

			if (! $user) {
				return;
			} elseif (method_exists($user, 'validateForPassportPasswordGrant')) {
				if (! $user->validateForPassportPasswordGrant($password)) {
					return;
				}
			} elseif (! $this->hasher->check($password, $user->getAuthPassword())) {
				return;
			}

			return new User($user->getAuthIdentifier());
		}
		```
	
	
		
   - Location: ```project-folder-name/symcom/api/vendor/league/oauth2-server/src/Grant/PasswordGrant.php```
		In this script do the following things:
       - Comment out the existing validateUser() function. like shown below:
		```
		// protected function validateUser(ServerRequestInterface $request, ClientEntityInterface $client)
		// {
		//     $username = $this->getRequestParameter('username', $request);
		//     if (is_null($username)) {
		//         throw OAuthServerException::invalidRequest('username');
		//     }

		//     $password = $this->getRequestParameter('password', $request);
		//     if (is_null($password)) {
		//         throw OAuthServerException::invalidRequest('password');
		//     }

		//     $user = $this->userRepository->getUserEntityByUserCredentials(
		//         $username,
		//         $password,
		//         $this->getIdentifier(),
		//         $client
		//     );
		//     if ($user instanceof UserEntityInterface === false) {
		//         $this->getEmitter()->emit(new RequestEvent(RequestEvent::USER_AUTHENTICATION_FAILED, $request));

		//         throw OAuthServerException::invalidCredentials();
		//     }

		//     return $user;
		// }
		```


       - Now add the new validateUser() function code which is given below. Just copy the below function and add it in PasswordGrant.php inside the class:
		```
		/**
		* Customised validateUser()
		* Default one is commented above
		**/
		protected function validateUser(ServerRequestInterface $request, ClientEntityInterface $client)
		{
			$username = $this->getRequestParameter('username', $request);
			if (is_null($username)) {
				throw OAuthServerException::invalidRequest('username');
			}

			$password = $this->getRequestParameter('password', $request);
			if (is_null($password)) {
				throw OAuthServerException::invalidRequest('password');
			}

			$provider = $this->getRequestParameter('provider', $request);
			if (is_null($provider)) {
				throw OAuthServerException::invalidRequest('provider');
			}

			$user = $this->userRepository->getEntityByUserCredentials(
				$username,
				$password,
				$this->getIdentifier(),
				$client,
				$provider
			);
			if ($user instanceof UserEntityInterface === false) {
				$this->getEmitter()->emit(new RequestEvent(RequestEvent::USER_AUTHENTICATION_FAILED, $request));

				throw OAuthServerException::invalidCredentials();
			}

			return $user;
		}
		```
		
		
		
-->
