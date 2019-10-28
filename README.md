# GifTastic

Technologies used:
HTML
CSS
Jquery
AJAX

This assignment has one HTML page with css and javascript:
1. gifTastic.html

This app will create buttons of the search items and when button is clicked will display ten still images relevant to the button
and when clicked on the image will make it gif.

In gifTastic page the following is the css block 
'''
 <style type="text/css">
    button,
    div,
    form,
    input,
    h1 {
      margin: 10px;
    }
    .movie{
      background: turquoise;
      color: white;
      border-radius: 4px;
    }
    #add-movie{
      background: turquoise;
      color: white;
      border-radius: 4px;
    }
   img{
       width: 150px;
       height: 150px;
   }
    #movie-form{
        float: right;

    }
    .rating{
      width: 200px;
      height: 200px;
      float: left;
      display: block;
    }
    #movie-form{
      height: 200px;
    }
    #movie-input{
      width: 275px;
    }
  </style>
'''
In gifTastic page the following is the html block 
'''
<div class="container">
    <h1>Movie Search</h1>
    <div id="buttons-view"></div>
    <form id="movie-form">
      <label for="movie-input"><b>Add a Movie</b></label>
      <br>
      <input type="text" id="movie-input"><br>
      <input id="add-movie" type="submit" value="Submit">
    </form>
    <div id="movies-view"></div>
'''
In gifTastic page the following is the javascript block 
'''
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
    <script type="text/javascript">
      var movies = ["coco", "cars", "toy story", "up", "monsters inc", "cars 2", "toy story 2", "inside out", "ratatouille", "finding nemo", "brave", "a bugs life"];
      function displayMovieInfo() {
        var movie = $(this).attr("data-name");
        var queryURL = "https://api.giphy.com/v1/gifs/search?q=" + movie + "&limit=10&api_key=vlcL7s4qPXsxTj6GgNON6UQyNAbmQIH5";
        $.ajax({
          url: queryURL,
          method: "GET"
        }).then(function(response) {          
            console.log(response);
            $("#movies-view").empty();
            for( var i = 0; i< response.data.length; i++){
              $("#movies-view").append("<div class= 'rating' id='movie"+ i + "'>");
              $("#movie"+ i ).append("<p> Rating :"+ response.data[i].rating + "</p>");
              $("#movie"+ i ).append("<img  data-state='still' data-still='"+ response.data[i].images.fixed_height_still.url + "' data-animated='"+ response.data[i].images.fixed_height.url + "' src=' " + response.data[i].images.fixed_height_still.url + "'"+ ">");
            }
        });
      }
      function renderButtons() {
        $("#buttons-view").empty();
        for (var i = 0; i < movies.length; i++) {
          var newButton = $("<button>");
          newButton.addClass("movie");
          newButton.attr("data-name", movies[i]);
          newButton.text(movies[i]);
          $("#buttons-view").append(newButton);
        }
      }
      $("#add-movie").on("click", function(event) {
        event.preventDefault();
        var movie = $("#movie-input").val().trim();
        var letters = /^[0-9a-zA-Z]+[ 0-9a-zA-Z]*$/;
       if(movie.match(letters)){
        movies.push(movie);
        }
        renderButtons();
      });
      $(document).on("click", ".movie", displayMovieInfo);
      $(document).on("click", "img", function(){
        var state = $(this).attr("data-state");
        if(state == "still"){
         $(this).attr("src", $(this).attr("data-animated"));
          $(this).attr("data-state", "animated");
        }else{
          $(this).attr("src", $(this).attr("data-still"));
          $(this).attr("data-state", "still");
        }
      });
      renderButtons();
    </script>
'''
screenshot of the page
gifTastic.html

![image]()


![image]()

![image]()


