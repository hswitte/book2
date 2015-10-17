# UI

Pick one question class and build an exploratory visualization interface for it.
The question class you pick must have at least three variables that can be changed.

## For a state X and ambience Y, how many businesses are there at each star rating?

<div style="border:1px grey solid; padding:5px;">
    <div><h5>State: X</h5>
        <input id="arg1" type="text" value="something"/>
    </div>
    <div><h5>Ambience: Y</h5>
        <input id="arg2" type="text" value="something"/> ("intimate", "classy", "hipster", "divey", "touristy", "trendy", "upscale", "casual" )
    </div>
    <div><h5>Z</h5>
        <input id="arg3" type="text" value="descending"/> ("ascending", "descending")
    </div>    
    <div style="margin:20px;">
        <button id="viz">Vizualize</button>
    </div>
</div>

<div class="myviz" style="width:100%; height:500px; border: 1px black solid; padding: 5px;">
Data is not loaded yet
</div>

{% script %}
items = 'not loaded yet'

console.log('lodash version:', _.VERSION)

$.get('http://bigdatahci2015.github.io/data/yelp/yelp_academic_dataset_business.5000.json.lines.txt')
    .success(function(data){        
        var lines = data.trim().split('\n')

        // convert text lines to json arrays and save them in `items`
        items = _.map(lines, JSON.parse)

        console.log('number of items loaded:', items.length)

        console.log('first item', items[0])
     })
     .error(function(e){
         console.error(e)
     })

function viz(arg1, arg2, arg3){    

    // define a template string
    var tplString = '<g transform="translate(0 ${d.y})"> \
                    <text y="20">${d.label}</text> \
                    <rect x="30"   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    </g>'

    // compile the string to get a template function
    var template = _.template(tplString)

    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {        
        return d[1].length * 7
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }

    function computeLabel(d, i) {
        return d[0]
    }

    var state = _.filter(items, function(d){
        return (d.state == arg1 && d.attributes && d.attributes.Ambience && d.attributes.Ambience[arg2])
        })
    console.log('filter', state)

    var groups = _.groupBy(state, "stars")
    console.log('groups', groups)

 
    var pairs = _.sortBy(_.pairs(groups), function(n){
        return n[0]
        })
    console.log(arg3)
    if (arg3 == 'descending') {pairs = pairs.reverse()}

    var viz = _.map(pairs, function(d, i){                
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i),
                    label: computeLabel(d, i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg width="100%" height="100%">' + result + '</svg>')
}

$('button#viz').click(function(){    
    var arg1 = $('input#arg1').val()
    var arg2 = $('input#arg2').val()
    var arg3 = $('input#arg3').val()   
    viz(arg1, arg2, arg3)
})  


{% endscript %}

# Authors

This UI is developed by
* [Kari Santos](https://github.com/karisantos)
* [Heather Witte](https://github.com/hswitte)
* [Zachary Lamb](https://github.com/ZachLamb)
* [Fadhil Suhendi](https://github.com/fadhilfath)
* [Denis Kazakov](https://github.com/94kazakov)
