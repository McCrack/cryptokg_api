<h1>Cryptokg API</h1>

<h3>Sending leads</h3>
<ol>
  <li>Before sending leads to the system, make sure that the source IP address is added to the whitelist</li>
  <li>Come up with a name for your affiliate in the format Source_Team_Geo. For example - FB_DreamTeam_CA</li>
  <li>Request an access token</li>
  <li>Send a POST request in JSON format to edpoint https://crm.cryptokg.io/api/v2/clients/create</li>
</ol>

<p>Request fields:</p>
<code><pre>
{
  "email": "", 
    "password": "",
    "first_name": "",
    "last_name": "",
    "phone": "",
    "country_code": "",
    "token": "zvtoz5egy8kmjtrslb76c8",
    "offer": "FB_Trafficgiants_RU",
    "comment": ""
}
</pre></code>
