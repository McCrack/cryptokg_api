<h1>Cryptokg API</h1>

<h3>Sending leads</h3>
<ol>
  <li>Before sending leads to the system, make sure that the source IP address is added to the whitelist</li>
  <li>Come up with a name for your affiliate in the format Source_Team_Geo. For example - FB_DreamTeam_CA</li>
  <li>Request an access token</li>
  <li>Send a POST request in JSON format to edpoint https://crm.cryptokg.io/api/v2/clients/create</li>
</ol>

<p>Request fields:</p>
<pre><code>
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
</code></pre>

<h4>Example implementation on PHP</h4>
<pre><code>
<?php


/** If the site sends data in JSON format */

// $data = file_get_contents('php://input');
// $payload = json_decode($data, true);
// $payload['country_code'] = "CA";
// $payload['token'] = "abcoz5egy8kmjtrslb67a5";
// $payload['offer'] = "FB_DreamTeam_CA";
// $payload['comment'] = "<ul><li>{$_SERVER['HTTP_HOST']}</li></ul>";

/** Else */

$payload = [
  'email' => $_POST['email'],
  'password' => $_POST['password'],
  'first_name' => $_POST['first_name'],
  'last_name' => $_POST['last_name'],
  'phone' => $_POST['phone'],
  'country_code' => 'CA',
  'token' => "abcoz5egy8kmjtrslb67a5",
  'offer' => "FB_DreamTeam_CA",
  'comment' => "<ul><li>{$_SERVER['HTTP_HOST']}</li></ul>",
];


$curl = curl_init();


try {
  $curl = curl_init();

  curl_setopt_array($curl, [
    CURLOPT_URL => "https://crm.cryptokg.io/api/v2/clients/create",
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'POST',
    CURLOPT_POSTFIELDS => json_encode($payload),
    CURLOPT_HTTPHEADER => [
      "Content-Type: application/json",
    ],
  ));

  $response = curl_exec($curl);
  curl_close($curl);

  if (empty($response)) {
    throw new \ErrorException("Can't make request");
  }

  print_r($response);
} catch (\ErrorException $exc) {
  http_response_code(400);
}


?>
</code></pre>

<h3>Getting information about leads</h3>
<p>Send a GET request to the https://crm.cryptokg.io/api/v2/leads endpoint with parameters: token, from, to. You can also specify the number of clients per page using the per_page parameter and the page number - the page parameter
If the &to= parameter is not specified, then the result will be all records up to the current moment</p>

<p>Example:</p>
<code>https://crm.cryptokg.io/api/v2/leads?token=abcoz5egy8kmjtrslb67a5&from=2022-10-01&to=2022-11-01&per_page=50&page=1</code>
<p>the response will contain the names and emails of clients, our internal ID, status and whether there was a deposit in the isFTD field</p>
