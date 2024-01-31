<div align="center">
  <img alt="Laradock" src="https://raw.githubusercontent.com/TianMeds/image--stocks-for-coding/main/image_2024-01-31_173621833.png" width="100%" height="auto" />
  <h1>How to install Laradock to your project</h1>

</div>

  <h3>So, right now we’re going to talk about how to install a Laradock or a dockerized Laravel application, but first, what is Laradock?</h3>

  <h1>Laradock</h1>
  <ul>
    <li>
      <p>Laradock simplifies the process of dockerizing Laravel applications, offering a convenient and efficient solution for developers. Dockerizing your Laravel project with Laradock allows you to encapsulate the entire development environment, making it portable and reproducible across different systems. This guide will walk you through the straightforward process of installing Laradock for your Laravel project. You can <a href="https://laradock.io">Visit Laradock Documentation</a> here</p>
    </li>
  </ul>

  <h1>Tools We need</h1>
  <ul>
  <li>Docker</li>
  <li>Visual Studio Code or any IDE you want</li>
  <li>Browser</li>
  <li>Composer Installed</li>
  <li>PHP Installed</li>
  </ul>

  <h1>Steps for Installing Laradock</h1>
<h4>Step 1: Create a folder of you want to create your file, so in my case i create a folder structure like this </h2>
<img alt="Folder Structure" src="https://raw.githubusercontent.com/TianMeds/image--stocks-for-coding/main/image_2024-01-31_175528055.png"/>
<h4>Step 2: So you should cd to your Backend Folder, so if you are in the Desktop this is how you will do it.</h4>
```
cd Main Folder
cd Backend Folder
```
<h4>Step 3: Clone Laradock to folder of choice </h4>

```
git clone https://github.com/Laradock/laradock.git
```
<h4>Step 4: Enter the Laradock folder created inside the Backend Folder, so it means that you will cd again after that rename .env.example to .env</h4>
```
cp .env.example .env
```
<h4>Step 5: Change PHP version in .env to 8.2</h4>
<img alt="PHP Version ENV" src="https://raw.githubusercontent.com/TianMeds/image--stocks-for-coding/main/image_2024-01-31_175425942.png"/>
<h4>Step 6: Run your Docker containers</h4>
```
docker-compose up -d nginx mysql phpmyadmin workspace
```
<h4>Step 7: Enter Workspace container, to run commands like artisan, phpunit</h4>
```
docker-compose exec workspace bash
```

<h4>Step 8: Create the project or the Laravel Application</h4>
```
composer create-project laravel/laravel `your-project-name`
```

<h4>Step 9: Create DB for the project</h4>
<ul>
  <li>Open phpMyAdmin, localhost:8081</li>
  <li>server: mysql</li>
  <li>username: root</li>
  <li>pass: root</li>
</ul>

<h4>Step 10: Create NGINX Configuration for the project</h4>
<p><i>Note you can name it all the way you i just make it consistent so not too hard to remember</i></p>

```
1. Open /nginx/sites/
2. Duplicate laravel.conf.example
3. Rename the duplicate to `your-project-name`.conf
4. Change these Lines 18-19
    server_name `your-project-name`; // add that to your machines /etc/hosts
    root /var/www/`your-project-name`/public;
```

<h4>Step 11: Now after that make sure to go to your /etc/hosts in your Unit for window users you can thru it by</h4>
```
C Drive -> Windows -> System32 -> Drivers -> etc -> hosts
```
<p><i>Note: Make sure to run the hosts as Administrator</i></p>


<p>After that edit the hosts file to like this and then saved it.</p>
```
--- hosts file ---

#End of section
127.0.0.1  `Name it on what you named in the step 10`
```

<h4>Step 12: Now Laravel Interface should be searchable and seen when you search it, It will be like this when you search it.</h4>
```
http://name-you-put-in-hosts-and-step10
```

<p>This is the output should look or make sure its accessible in short</p>

<img alt="Laravel Interface" src="https://raw.githubusercontent.com/TianMeds/image--stocks-for-coding/main/image_2024-01-31_175442083.png"/> 

<p><b>Bonus Issues we resolve in the process</b></p>

<h1>Issues</h1>

<h4>First Issue: 404 not found:: Can’t access the static Laravel front-end</h4>
<p><i>Ensure that Nginx has the necessary permissions to access the files in your Laravel project. The Nginx process needs to have read permissions for the files and execute permissions for the directories.</i></p>

```
docker-compose exec workspace chmod -R 755 /var/www/your-project-name
```

<h4>Second Issue: laravel — The stream or file “/storage/logs/laravel.log” could not be opened in append mode: failed to open stream: Permission denied</h4>
```
/var/www/`project-name`#  sudo chmod -R ugo+rw storage
```

<h1>Notes</h1>
<ul>
<li>Rebuilding a container</li>
</ul>

```
docker-compose build `container` 
docker-compose build workspace
```

<ul>
<li>Recreating a container</li>
</ul>

```
docker-compose up -d `container`
docker-compose up -d workspace
```


  
