dangerzone
==========

Inline bug tracker snapped into any site for simple and elegant bug/task tracking. 
----------------------------------------------------------------------------------

I need a very simple bug tracker for my personal 
projects. I don't need a dedicated site for it, 
I need it to be: a) inline,  
  b) simple, and  
  c) at my finger-tips. 
  
So I entered the zone of danger and built this little bugger.

So far, it's just a [Flask] [1] app, that you hook into your application like so:

    # application.py
    from dangerzone import kennyrogers
  
Hah, of course it cannot be that easy ("or can it!?", "CAN IT, JOHN."). 

    # dangerzone.py  
    class kennyrogers:
      def debugger(request):
        if request.method == "GET" and request.args.get('dz') == '1':
          dangerzone = '<script type="text/javascript">/* minified js goes here inline */</script>'
        else:
          dangerzone = ""
        return dangerzone
  
And in the application (flask app or whatever plops your data to the view)
  
    # application.py
    @app.route('/')
    def index():
      return render_template("kenny_rogers_extends_base.html", DANGERZONE=kennyrogers.debugger(request))
    
And, of course we have to add this to the base template that all other pages extend. You have one of those, right, James?
  
    # base_template.html
    <!--
    [...] some html here [...]
      -->
    {% if dangerzone %}
      {% DANGERZONE %}
    {% endif %}
    
Now access your app with http://localhost/whatever?dz=1 and you too will be in the zone of danger. Now fix some bugs. Do some stuff. Have at it, you.

[1]: http://flask.pocoo.org/ "Flask project page"