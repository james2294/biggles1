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
