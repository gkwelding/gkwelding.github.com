---
comments: true
date: 2009-10-23 15:10:46
layout: post
slug: create-your-own-custom-php-session-handler
title: Create Your Own Custom PHP Session Handler
summary: Create Your Own Custom PHP Session Handler
wordpress_id: 40
image: placeholder.jpg
tags:
- php
- tips
- work
---

Now I'm a big believer in that you can learn more from observing the code than you can from being told or taught something by somebody else. I've added the code below for a simple custom session handler than saves session info into the database. Read and work through this, if you're really stuck with anything look on php.net, if you're really really stuck with anything then Google it, if you're really really really stuck and you've asked your dog and your granny and they don't know then post a comment below and I'll get back to you about it.

File: test.php

[sourcecode lang="php"]

Unrecognized handler ($handler)";
die;
}

/* start the session and register a simple counter */
session_start();
session_register("count");

/* figure out what we should do, depending on the action */
switch ($action) {
case "increment" :
$count = isset($count) ? $count + 1 : 0;
break;

case "destroy" :
session_destroy();
break;

case "gc" :
$maxlife = get_cfg_var("session.gc_maxlifetime");
sess_gc($maxlife);
break;

default:
echo "
* Unknown action ($action)";
break;
}
?>



# Session Test Script






  * Handler: ****

  * Action: ****

  * Count: ****




* * *










Handler:




DBM
MySQL








Action:




Increment
Session Destroy
Force Garbage Collection










  






[/sourcecode]

File: session_dbm.php

[sourcecode lang="php"]

time()) {
$var = substr($tmp, strpos($tmp, "|") + 1);
}
}

return $var;
}

function sess_write($key, $val) {
global $SESS_DBM, $SESS_LIFE;

dbmreplace($SESS_DBM, $key, time() + $SESS_LIFE . "|" . $val);
return true;
}

function sess_destroy($key) {
global $SESS_DBM;

dbmdelete($SESS_DBM, $key);
return true;
}

function sess_gc($maxlifetime) {
global $SESS_DBM;

$now = time();

$key = dbmfirstkey($SESS_DBM);
while ($key) {
if ($tmp = dbmfetch($SESS_DBM, $key)) {
$expires_at = substr($tmp, 0, strpos($tmp, "|"));
if ($now > $expires_at) {
sess_destroy($key);
}
}

$key = dbmnextkey($SESS_DBM, $key);
}
}

session_set_save_handler(
"sess_open",
"sess_close",
"sess_read",
"sess_write",
"sess_destroy",
"sess_gc");
?>

[/sourcecode]

File: session_mysql.php

[sourcecode lang="php"]

Can't connect to $SESS_DBHOST as $SESS_DBUSER";
echo "
* MySQL Error: ", mysql_error();
die;
}

if (! mysql_select_db($SESS_DBNAME, $SESS_DBH)) {
echo "
* Unable to select database $SESS_DBNAME";
die;
}

return true;
}

function sess_close() {
return true;
}

function sess_read($key) {
global $SESS_DBH, $SESS_LIFE;

$qry = "SELECT value FROM sessions WHERE sesskey = '$key' AND expiry > " . time();
$qid = mysql_query($qry, $SESS_DBH);

if (list($value) = mysql_fetch_row($qid)) {
return $value;
}

return false;
}

function sess_write($key, $val) {
global $SESS_DBH, $SESS_LIFE;

$expiry = time() + $SESS_LIFE;
$value = addslashes($val);

$qry = "INSERT INTO sessions VALUES ('$key', $expiry, '$value')";
$qid = mysql_query($qry, $SESS_DBH);

if (! $qid) {
$qry = "UPDATE sessions SET expiry = $expiry, value = '$value' WHERE sesskey = '$key' AND expiry > " . time();
$qid = mysql_query($qry, $SESS_DBH);
}

return $qid;
}

function sess_destroy($key) {
global $SESS_DBH;

$qry = "DELETE FROM sessions WHERE sesskey = '$key'";
$qid = mysql_query($qry, $SESS_DBH);

return $qid;
}

function sess_gc($maxlifetime) {
global $SESS_DBH;

$qry = "DELETE FROM sessions WHERE expiry < " . time();
$qid = mysql_query($qry, $SESS_DBH);

return mysql_affected_rows($SESS_DBH);
}

session_set_save_handler(
"sess_open",
"sess_close",
"sess_read",
"sess_write",
"sess_destroy",
"sess_gc");
?>

[/sourcecode]
