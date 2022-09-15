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
- Click *"Try it out"*, add "\*" in the origin field, then click *"Execute"*:

<p align="center">
  <br>
  <img src="getting_started/_media/cors_1.png" style="width:30%" />
  <br>
</p>

- You will be asked to log in. Use your admin login.
- Verify that the server responds with a *204* HTTP code:

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
      <button id="btn-test"
         class="btn btn-success btn-lg float-right" 
         type="submit"> 
      Test  
      </button> 
   </div>
</div>

## Get the certificates
<div class="form-group"> 
      <button id="btn-certs"
         class="btn btn-success btn-lg float-right" 
         type="submit"> 
      Get certificates  
      </button> 
</div>

## Run the demo endpoint java

## Read the data
If not done automatically at the previous step, please entre your endpoint UUID below. 
By hitting the start button, you will enable the polling of the attribute *"myNode/myObject/myMeasure"* value.
<div class="container">
   <table>
      <tr>
         <th>UUID</th>
      </tr>
      <tr>
         <td><input id="uuid"
            class="form-control" 
            type="text" 
            placeholder="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"> </td>
      </tr>
   </table>
   <div class="form-group"> 
      <button id="btn-read"
         class="btn btn-success btn-lg float-right" 
         type="submit"> 
      Start  
      </button> 
	  <output id="attribute"><b>/myNode/myObject/myMeasure:</b> </output>
   </div>
</div>
<iframe id="download_frame" style="display:none;"></iframe>


> Note: For performance reasons, the attributes values are stored every 3s in influxDB, that's why you can't see every value changes. 
If necessary, you can connect through Stomp/Websocket or MQTT to get notified on every change.

?> Question

<script type="text/javascript">
	
	$(document).ready(function () {		
	  var timer = null;
	  
	  $("#btn-test").click(function () {
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
					alert("Connection successful!");
				},
				error: function (jqXHR, textStatus, errorThrown)
				{
					alert("Error while trying to connect");
				}
			});
		}
	  });
	  $("#hostname").on("input", function () {		
			$("#swagger_url").text($("#hostname").val() + "/swagger-ui/index.html#/Cors Management/postOrigin").show();
			$("#swagger_url").attr("href", $("#swagger_url").text());
		});
		
	  $("#btn-certs").click(function () {
		var host = $("#hostname").val();
		var user = $("#username").val();
		var pass = $("#password").val();
		var uuid = "";
		
		if(!host)
			alert("Hostname cannot be empty!");
		else if(!user)
			alert("Username cannot be empty!");
		else if(!pass)
			alert("Password cannot be empty!");
		else{	
			var formData = {};
			$.ajax({
				url : host + "/api/v1/endpoints?friendlyName=quickstart",
				type: "POST",
				data : formData,
				crossDomain: true,
				headers: {
					"Authorization": "Basic " + btoa(user + ":" + pass)
                },
				success: function(data, textStatus, jqXHR)
				{
					uuid = data.uuid;
					$("#uuid").val(uuid);
					
					set_properties(host, user, pass, uuid);
				},
				error: function (jqXHR, textStatus, errorThrown)
				{
					alert("Error while creating endpoint");
				}
			});
		}
	  });
		
	  $("#btn-read").click(function () {
		var host = $("#hostname").val();
		var user = $("#username").val();
		var pass = $("#password").val();
		var uuid = $("#uuid").val();
		
		if($("#btn-read").text() === "Start"){
				if(!host)
					alert("Hostname cannot be empty!");
				else if(!user)
					alert("Username cannot be empty!");
				else if(!pass)
					alert("Password cannot be empty!");
				else if(!uuid)
					alert("UUID cannot be empty!");	
				else{
					$("#btn-read").html("Stop");
						timer = setInterval(function(){
						const attr = read_attribute(host, user, pass, uuid + "/myNode/myObject/myMeasure", display_my_measure);						
					}, 3000);					
				}
		}
		else{
			$("#btn-read").html("Start");
			clearInterval(timer);
			timer = null;
		}
	  });
	});
	function read_attribute(host, user, pass, attr, _callback) {
		var formData = {};
			$.ajax({
				url : host + "/api/v1/data/" + attr,
				type: "GET",
				data : formData,
				crossDomain: true,
				headers: {
					"Authorization": "Basic " + btoa(user + ":" + pass)
                },
				success: function(data, textStatus, jqXHR)
				{
					console.log(data);
					_callback(attr, data);
				},
				error: function (jqXHR, textStatus, errorThrown)
				{
					alert("Error while trying to reading data");
				}
			});
    }
	
	function display_my_measure(id, value) {
		console.log(id + ": " + value.value);
		$("#attribute").html("<b>myNode/myObject/myMeasure:</b> " + value.value);
	}
	
	function set_properties(host, user, pass, uuid) {
		var tab = host.replace("http://", "").replace("https://", "").split(":");
		var formData = {
		  "customProperties": {
			"ch.hevs.cloudio.endpoint.hostUri": "ssl://" + tab[0],
			"ch.hevs.cloudio.endpoint.ssl.authorityCert": "file:/C:/Users/.../cloudio-endpoint-java-example/src/main/resources/cloud.io/authority.jks",
			"ch.hevs.cloudio.endpoint.ssl.clientCert": "file:/C:/Users/.../cloudio-endpoint-java-example/src/main/resources/cloud.io/" + uuid + ".p12",
			"ch.hevs.cloudio.endpoint.ssl.verifyHostname": "false"
		  }
		};
		console.log(formData);
		$.ajax({
			url : host + "/api/v1/endpoints/" + uuid + "/provisionToken",
			type: "POST",
			data : JSON.stringify(formData),
			crossDomain: true,
			headers: {
				"Authorization": "Basic " + btoa(user + ":" + pass),
				"Content-Type": "application/json"
			},
			success: function(data, textStatus, jqXHR)
			{
				get_certificates(host, data);
			},
			error: function (jqXHR, textStatus, errorThrown)
			{
				alert("Error while trying to generate certificates");
			}
		});
    }
	
	function get_certificates(host, token){
		
		fetch(host + "/api/v1/provision/" + token, {headers: {"Accept": "application/java-archive"}})
		  .then(resp => resp.blob())
		  .then(blob => {
			const url = window.URL.createObjectURL(blob);
			const a = document.createElement('a');
			a.style.display = 'none';
			a.href = url;
			// the filename you want
			a.download = 'quickstart-certificates.zip';
			document.body.appendChild(a);
			a.click();
			window.URL.revokeObjectURL(url);
		  })
		  .catch(() => alert('Error while downloading the certificates!'));
	}

</script>

