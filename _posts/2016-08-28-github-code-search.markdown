---
layout: default
title:  "GitHub Code Search"
date:   2016-08-27 17:50:00
categories: main
---
<form  >
<input id="github_search" class="github-search" type="search" name="search github code" placeholder="search github code"  />
</form>
<div id="results"></div>
<script>
$( "form" ).submit(function( event ) {
  event.preventDefault();
  var search_text = $("#github_search").val().trim();
  if ( search_text.length===0 ) {
    $( "span" ).text( "Enter Search text..." ).show().fadeOut( 1000 );;
    return;
  }
  $("#results").text("Searching........");
  $.getJSON( "https://api.github.com/search/code?q="+search_text.trim()+"+in:file+language:js+repo:jquery/jquery", function( data ) {

    var items = [];
    $.each( data.items, function( index, value ) {
      items.push(
         "<li id='" + index + "'><a href=" +value.html_url + "  target='_blank'>" +value.name + "</a></li>" );
    });
$("#results").text("Result.......\n");
    $( "<ul/>", {
      "class": "my-new-list",
      html: items.join( "" )
    }).appendTo( "#results" );

});
});
</script>
