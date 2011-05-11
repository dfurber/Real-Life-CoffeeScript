!SLIDE incremental bullets
# What are the features? 
* Easy variable declaration (lexical scoping)
* Easy class inheritance and binding
* Easy instance variables @name => this.name
* Implicit return from functions
* "String #{interpolation}"

!SLIDE incremental bullets
# Semantic Shortcuts 
* -> and => instead of function(){}
* execute() if that is thing1 and that isnt thing2
* and/or/not instead of &&/||/!
* that = thing1 or thing2
* that or= thing3

!SLIDE incremental bullets
# Conditionals 
* if condition? (no parantheses, ? is .nil? not .blank?)
* if condition?() to evaluate if a function returns null
* throwAFit() unless @name in ["Paul", "John"]

!SLIDE incremental bullets
# How much more? 
* list traversal: for result in results
* return (transform result for result in results)
* switch/when/else instead of switch/case/default
* yes/no, on/off for true/false

!SLIDE center
## Show me some code!

!SLIDE code smaller
# Some ugly JavaScript
    @@@ JavaScript
    var sortFunction = function(a,b) {
        if (typeof(a[sort_col]) === 'number') {
            // numeric sort
            if (sort_dir === 'up') return (a[sort_col] - b[sort_col]);
            else                   return (b[sort_col] - a[sort_col]);
        } else {
            // string sort
            var aName = a[sort_col].toLowerCase(), bName = b[sort_col].toLowerCase();
            if (sort_dir === 'up') return (aName > bName);
            else return (bName > aName);
        }
    }

    this.getResults = function(){
        // here is the place to apply filter
        var results = parent.results;
        if (filter_text) {
            results = $.makeArray($.map(results, function(result, i){
                var haystack = [result.name, result.brands, result.address, result.city].join(', ')
                return (haystack.indexOf(filter_text) != -1) ? result : null;
            }));
        }
        if (sort_col && sort_dir) {
            results = results.sort(sortFunction);
        }
        return results;
    }

!SLIDE code smaller
    @@@ Ruby
    class Results
        setSort: (col, dir) ->
            if col? and dir?
                results = _(@results).sortBy (result) -> result[col]
                @results = if dir is 'down' then results.reverse() else results
        setFilter: (filter) ->
            if filter?
                matching = (needle) ->
                    haystack = _.join needle.name, needle.brand_list, needle.address, needle.city
                    _(haystack).includes(needle)
                @results = _.select @results, matching
        
!SLIDE code smaller
# standard jQuery with object binding
    @@@ Ruby
    $('#view_as_table').click  => @.setViewType('Table', true)
    $('#view_as_thumbs').click => @.setViewType('Thumb', true)
    $('#view_as_list').click   => @.setViewType('List', true)
    
!SLIDE code smaller
# Big Long jQuery Call
    @@@ Ruby
    var makeSortable = function(){
        $('#widgets .col').sortable({
            items: 'div.widget',
            dropOnEmpty: true,
            handle: '.header h3',
            appendTo: 'body',
            connectWith: '.col',
            ...
        });

    makeSortable = ->
        $('#widgets .col').sortable
            items: 'div.widget'
            dropOnEmpty: yes
            handle: '.header h3'
            appendTo: 'body'
            connectWith: '.col'
            revert: yes
            cursor: 'move'
            placeholder: 'drag-over'
            stop: updateWidgetOrder

!SLIDE code smaller
    @@@ Ruby
    class JKT.GoogleLoader
        constructor: (callback) ->
            @callback = callback
            if google? then @loadComponent() else @loadGoogle()

        loadComponent: -> return
        loadGoogle: () ->
            script = document.createElement "script"
            script.src = "http://www.google.com/jsapi?key=#{JKT.google_api_key}&sensor=false"
            script.type = "text/javascript"
            if script.attachEvent? # IE
                script.attachEvent 'onreadystatechange', =>
                    if script.readyState in ['loaded', 'complete']
                        @loadComponent()
            else
                script.onload = => @loadComponent()
            document.getElementsByTagName("head")[0].appendChild(script)
    

    class JKT.MapLoader extends JKT.GoogleLoader
        loadComponent: ->
            google.load 'maps', '3', 
                other_params: "sensor=false"
                callback: @callback
            return

!SLIDE code smaller
# super Is Super #
    @@@ Ruby
    class JKT.Search.TableRenderer
        constructor: (results) -> @results = results
        render: ->
            $('#results').html $('#listing_grid').render [{foo:"bar"}]
            $('#results tbody').html $('#listing_grid_row').render(@results)

    class JKT.Search.MapRenderer extends JKT.Search.TableRenderer
        render: ->
            super
            if @results.length <= 300
                $('#results tbody tr').each ->
                    ...
                    
!SLIDE code smaller
    @@@ Ruby
    class Results
        ...
        paginate: (start, end) ->
            if start? and end?
                @results = @results[start..end]

        toSentence: -> 
            size = _.size(@results) or 0
            if size is 1 then "1 result" else \
                "#{size} results"

        enoughForMap: -> _.size(@results) < 300
        any         : -> _.isArray(@results) and _.any(@results)
            

