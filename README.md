# Ask
Android runtime permissions make easy

# Why?

After in marshmallow android has introduced runtime permission check that means when application runs every time application needs to ask for perticular
permissions from user to run specific functionality. for example if you using Camera or saving files on external storage or location.

The android basic code to request permission is to complex and tedious to understand. Ask is a library make asking for the particular permission
easy for developer. This is very simple and light wait library with just few lines of code and you good to go.

## How to use.

Very first step is to include this library in your project by adding following entry into your project's gradle dependencies

```groovy
dependencies {
	compile 'com.vistrav:ask:1.0'
}
```

After adding the necessary permissions into your manifest file,
Add the following code in your class and that is all you need. You can do all you want in `granted` or `denied` methods

```java
        Ask.on(context)
                .forPermissions(Manifest.permission.ACCESS_COARSE_LOCATION
                        , Manifest.permission.WRITE_EXTERNAL_STORAGE) //one or more permissions
                .withRationales("Location permission need for map to work properly", 
                        "In order to save file you will need to grant storage permission") //optional
                .when(new Ask.Permission() {
                    @Override
                    public void granted(List<String> permissions) {
                        Log.i(TAG, "granted :: " + permissions);
                    }

                    @Override
                    public void denied(List<String> permissions) {
                        Log.i(TAG, "denied :: " + permissions);
                    }
                }).go();

```

The callback methods `granted` or `denied` will be called when permissions are granted or denied respectively with list of permissions as argument.
you can then write your logic in these method based of permission granted or denied.

The setting rationale message is optional but it would be good in case user has declined the permission, there is chance for developer to explain
app user why specific permission is needed

`forPermissions` take one or more permissions as argument
`withRationales` take one or more rationale message, usually it is good to provide same number of rationale messages as number of permissions


##You can contribute!
In case you think you have some improvement, please feel free do pull request your feature and I would be happy to include it. Let's make this Ask very easy to use and rich with features.

##License

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
