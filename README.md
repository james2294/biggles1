# biggles1
"""
This script runs the application using a development server.
It contains the definition of routes and views for the application.
"""

from flask import Flask, render_template, redirect, url_for, request, jsonify;
app = Flask(__name__)

# Make the WSGI interface available at the top level so wfastcgi can get it.
wsgi_app = app.wsgi_app


@app.route('/')
def home():
        return """<html>
    <head>
<title>home</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="static/global.css" rel="stylesheet" media="screen">
    <script src="{{url_for('static1', filename= 'jquery-2.2.3.min.js')}}" ></script>
    <script src="{{url_for('static1', filename= 'general.js')}}"></script>
</head>

<body>
     <div id="header">
          <div class="logo"><a href="#">James<span>Hunt</span><a></div>

          
     </div>
     
     <a class="mobile" href="#">MENU</a>
      
          <div id="container">
      <div class="sidebar">
      		<ul id="nav">
      			<li><a href="products">products</a></li>
      			<li><a href="boxsize">boxsize</a></li>
      			<li><a href="purchase">purchase</a></li>
                  <li><a class="mail" href="mailto:jameshunt927@gmail.com">Email </a>

      			</ul>

</div>
      <div class="content">
      		<h1>Home Products page</h1>
      		<p> This provides information on a range of products this web site has available to purchase </p>

      		<div id= "box">
              	<div class="box-top">Customer news</div>
      			<div class="box-panel">
      				This is more space from text information	
      			</div>
                  <div id= "box">
              	<div class="box-top">Customer news</div>
      			<div class="box-panel">
      				This is more space from text information	
      			</div>
                  <div id= "box">
              	<div class="box-top">Customer news</div>
      			<div class="box-panel">
      				Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum
                      	
      			</div>

     </div> 
                   </body>
            
    </html>"""

@app.route('/products')
def products():
    return render_template('products.html');

@app.route('/boxsize')
def boxsize():
    return render_template('boxsize.html');

@app.route('/purchase')
def purchase():
    return render_template('purchase.html'); 

@app.route('/login', methods=['GET', 'POST'])
def login():
    error = None
    if request.method == 'POST':
        if request.form['username'] != 'admin'or request.form['password'] != 'admin':
            error = 'invalid credentials. please try again.'
        else:
            return redirect(url_for('home'));
   
    return render_template('login.html' , error=error);




if __name__ == '__main__':
    import os
    HOST = os.environ.get('SERVER_HOST', 'localhost')
    try:
        PORT = int(os.environ.get('SERVER_PORT', '5555'))
    except ValueError:
        PORT = 5555
    app.run(HOST, PORT)


<!DOCTYPE html>

<html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title>products</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="static/global.css" rel="stylesheet" media="screen">
</head>
<body>
    <div class="content">
        <h1>range of products</h1>
        <p> this space is for text information about types of products available </p>
        <br>
        <p>click <a href="/">here</a> to go home</p>
        
        <div id="box">
            <div class="panel-top">product news</div>
            <div class="panel center">
                This is more space from text information
            </div>

        </div>
</body>
</html>


<!DOCTYPE html>

<html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title>boxsize</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="static/global.css" rel="stylesheet" media="screen">
</head>
<body>
    <div class="content">
        <h1>number and size of available boxes</h1>
        <p> this space is for text information about veg box delivery </p>
        <br>
        <p>click <a href="/">here</a> to go home</p>

                <div id="box">
            <div class="panel-top">packaging news</div>
            <div class="panel center">
                This is more space from text information
            </div>

        </div>
</body>
</html>


<!DOCTYPE html>

<html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title>purchase</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="static/global.css" rel="stylesheet" media="screen">
</head>
<body>
    <div class="content">
        <h1>purchase products</h1>
        <p> this space is for text information about purchase methods and cost </p>
        <br>
        <p>click <a href="/">here</a> to go home</p>
        </div>

        <div id="box">
            <div class="panel-top">product available to purchase news</div>
            <div class="panel center">
                This is more space from text information
            </div>

     </body>
</html>


<!DOCTYPE html>

<html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title>login</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="static/global.css" rel="stylesheet" media="screen">
</head>
<body>
    <div class="container">
        <h1>please login</h1>
        <br>
        <form action="" method="post">
            <input type="text" placeholder="username" name="username" value="{{ request. form.username }}">
            <input type="password" placeholder="password" name="password" value="{{request.form.password }}">
           <input class="btn btn-default" type="submit" value="login">
         </form>
        {% if error %}
        <p class="error"><strong>error:</strong> {{ error}}</p>
        {% endif%}
        </div>

</body>
</html>


$(document).ready(function(){
    $("a.mobile").click(function(){
        $(".sidebar").slideToggle('fast');
    });

    window.onresize = functio(event) {
        if($(window).width() > 321) {
            $(".sidebar").show();
        }
    };
});



* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
body {
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;

}

div#header {
    width: 100%;
    height: 50px;
    background-color:cornflowerblue;
            margin: 0 auto;

 }

.logo {
    float: left;
    margin-top: 10px;
    margin-left: 10px;
}

.logo a {
    font-size: 1.5em;
    color: azure;
}
    
.logo a span {
    font-weight: 300;


}    
div#container {
    width: 100%;
    margin: 0 auto;
}    
.sidebar {
    width: 240px;
    height: 100%;
    background-color:antiquewhite;
    float: left;
}
.content {
    width: auto;
    margin-left: 260px;
    height: 100%;
    background-color: burlywood;
    padding: 15px;
}

.content p {
    color:dimgrey;
    font-size: 0.75em;
}

div#box {
    margin-top: 15px;
}

div#box .box-top {
    color:dimgrey;
    text-shadow: 0px 0px 1px #808080;
    background-color: antiquewhite;
    padding: 25px;
    padding-left: 15px;
    font-weight:400; 
}

div#box .box-panel {
    padding: 25px;
    background-color:beige;



}

ul#nav {

} 

ul#nav li {
    list-style: none;
}

ul#nav li a {
    color:darkblue;
    display: block;
    padding: 15px;
    font-size: 1.2em;
    border-bottom: 1px solid:black;
    transition: 0.2s;
}

ul#nav li a:hover {
    background-color:darkolivegreen;
    color:darkseagreen;
    
} 

.content {
    width: auto;
    margin-left: 250px;
    height: 100%;

}

a.mobile {
    display: block;
    color:antiquewhite;
    background-color:black;
    text-align: center;
    padding: 10px;
    border-bottom: 2px 

}

a.mobile:active {
    background-color:darkgrey;
} 

@media only screen and (max-width:321px) {
    .sidebar {
        width: 100%;
        display:none;
    }
}
    .content {
    margin-left: 0px;
}
@media only screen and (min-width:321px) {
    
    a.mobile {
        display: none;
    }   
  
  
  
