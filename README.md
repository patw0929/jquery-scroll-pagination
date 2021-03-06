jQuery Scroll Pagination
====

Fork from https://github.com/andferminiano/jquery-scroll-pagination


***

Example of usage
---

           $(function(){
                $('#content').scrollPagination({
                    'contentPage': 'democontent.html', // the url you are fetching the results
                    'contentData': {}, // these are the variables you can pass to the request, for example: children().size() to know which page you are
                    'scrollTarget': $(window), // who gonna scroll? in this example, the full window
                    'heightOffset': 10, // it gonna request when scroll is 10 pixels before the page ends
                    'beforeLoad': function(){ // before load function, you can display a preloader div
                        $('#loading').fadeIn();
                    },
                    'afterLoad': function(elementsLoaded){ // after loading content, you can use this function to animate your new elements
                         $('#loading').fadeOut();
                         var i = 0;
                         $(elementsLoaded).fadeInWithDelay();
                         if ($('#content').children().size() > 100){ // if more than 100 results already loaded, then stop pagination (only for testing)
                            $('#nomoreresults').fadeIn();
                            $('#content').stopScrollPagination();
                         }
                    },
                    'nomoreData': function () {
                         $('#content').stopScrollPagination();
                    }
                });

                // code for fade in element by element
                $.fn.fadeInWithDelay = function(){
                    var delay = 0;
                    return this.each(function(){
                        $(this).delay(delay).animate({opacity:1}, 200);
                        delay += 100;
                    });
                };

            });



Example
---
            $('#loading').hide();

            var year = document.getElementById('sYear').value;

            $('#table-GrayGradient').scrollPagination({
                'contentPage': "/Management/Resolution/", // the page where you are searching for results
                'contentData': {}, // you can pass the children().size() to know where is the pagination
                'scrollTarget': $(window), // who gonna scroll? in this example, the full window
                'heightOffset': 10, // how many pixels before reaching end of the page would loading start? positives numbers only please
                'beforeLoad': function () { // before load, some function, maybe display a preloader div
                    window.page++;
                    this.contentPage = "/Management/Resolution/?sPage=" + window.page + "&sYear=" + year;
                    $('#loading').fadeIn();
                },
                'afterLoad': function (elementsLoaded) { // after loading, some function to animate results and hide a preloader div
                    $('#loading').fadeOut();
                    $(elementsLoaded).fadeInWithDelay();
                    box_resizes();
                },
                'nomoreData': function () {
                    $('#table-GrayGradient').stopScrollPagination();
                }
            });
            
            // code for fade in element by element
            $.fn.fadeInWithDelay = function () {
                var delay = 0;
                return this.each(function () {
                    $(this).delay(delay).animate({ opacity: 1 }, 200);
                    delay += 100;
                });
            };


***

Thank you for using it!
