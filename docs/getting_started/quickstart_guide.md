# Quickstart Guide

## Prerequesites

- A running cloud.iO services instance. See the getting started guide: [Deploy cloud hosted infrastructure](/deploy/deploy).
- Java JDK 11+ installed.

Please, enter your cloud.iO servers hostname:
<div class="container">
<table>
      <tr>
         <th>Hostname</th>
      </tr>
      <tr>
         <td><input id="hostname"
            class="form-control" 
            type="text" 
            placeholder="http://127.0.0.1:8080"></td>
      </tr>
   </table>
</div>

## Set the CORS policy

This guide will send HTTP REST commands to your cloud.iO server. To allow a webpage to communicate with the cloud.iO server, 
you have to set up its CORS policy (more information can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)).

- To do this, connect to the cloud.iO Swagger UI at 
<body>
	
	<a id="swagger_url" target="_blank" href="your_server_ip:8080/swagger-ui/index.html#/Cors Management/postOrigin">your_server_ip:8080/swagger-ui/index.html#/CorsManagement/postOrigin</a>
</body>
- Click "Try it out", add "\*" in the origin field, then click "Execute":

<p align="center">
  <br>
  <img src="getting_started/_media/cors_1.png" style="width:30%" />
  <br>
</p>

- You will be asked to log in. Use your admin login.
- Verify that the server responds with a 204 HTTP code:

<p align="center">
  <br>
  <img src="getting_started/_media/cors_2.png" style="width:40%" />
  <br>
</p>

!> All origins are now accepted. It is recommended to not use this CORS configuration in a production environnement.

Check that everything is correctly set up by testing the connection with the server:

<div class="container">
   <table>
      <tr>
         <th>Username</th>
         <th>Password</th>
      </tr>
      <tr>
         <td><input id="username"
            class="form-control" 
            type="text" 
            placeholder="admin"> </td>
         <td><input id="password"
            class="form-control" 
            type="password" 
            placeholder="password"> </td>
      </tr>
   </table>
   <div class="form-group"> 
      <button id="btn-certs"
         class="btn btn-success btn-lg float-right" 
         type="submit" style="background-color: #188AC7;
		  border: none;
		  color: white;
		  padding: 10px 32px;
		  text-align: center;
		  text-decoration: none;
		  display: inline-block;
		  font-size: 14px;"> 
      Test  
      </button> 
   </div>
</div>

<script type="text/javascript">
	$(document).ready(function () {		
	  $("#btn-certs").click(function () {
		var host = $("#hostname").val();
		var user = $("#username").val();
		var pass = $("#password").val();
		if(!host)
			alert("Hostname cannot be empty!");
		else if(!user)
			alert("Username cannot be empty!");
		else if(!pass)
			alert("Password cannot be empty!");
		else{	
			var formData = {};
			$.ajax({
				url : host + "/api/v1/account",
				type: "GET",
				data : formData,
				crossDomain: true,
				headers: {
					"Authorization": "Basic " + btoa(user + ":" + pass)
                },
				success: function(data, textStatus, jqXHR)
				{
					alert("Successful connected!")
				},
				error: function (jqXHR, textStatus, errorThrown)
				{
					alert("Error while trying to connect")
				}
			});
		}
	  });
	  $("#hostname").on("input", function () {		
			$("#swagger_url").text($("#hostname").val() + "/swagger-ui/index.html#/Cors Management/postOrigin").show();
			$("#swagger_url").attr("href", $("#swagger_url").text());
		});
	});
</script>

## Get the certificates

## Run the demo endpoint


> Information

?> Question



