
# ofxCEF

an attempt to get CEF working in openframeworks as an alternative to awesomium, berkelium, etc.   [More info on CEF](https://bitbucket.org/chromiumembedded/cef) [wiki](https://bitbucket.org/chromiumembedded/cef/wiki/Home)

## oddities: 

### OSX and Xcode

we have some issues closing the app because of some awkwardness with autorelease pool ([more info](http://www.magpcss.org/ceforum/viewtopic.php?f=6&t=11441&p=24037&hilit=AutoreleasePoolPage#p24037)).  Thus we do some tomfoolery in ofMain to init CEF before OF, and pass things around. 

Also, because of how CEF works, you will need to compile the helper app first

![image](images/helper.png)

then compile the demo app itself

![image](images/app.png)

### Windows and Visual Studio
* Tested with Windows 10, Visual Studio 15 and cef_binary_3.2987.1601.gf035232_windows32

* Copy the content of the Chromium Embedded Framework 3 Build package into the folder libs/CEF/win32. 
* Create VS project files by running cmake -G "Visual Studio 15" -DUSE_SANDBOX=Off from a Visual Studio command prompt in ofxCEF/libs/CEF/win32. -REQUIRES cmake V3.7.0
* Open cef.sln and changed the C/C++ Code Generation properties for all projects to /MDd (debug) or /MD (release)
* Build cef.sln - don't worry that ceftests doesn't build because of sandbox issues.
* Check cefsimple and cefclient run OK
* You should now be able to build and run example_ofxCEF