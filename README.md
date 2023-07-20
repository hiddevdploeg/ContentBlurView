# ContentBlurView
Easily get a fancy looking gradient blur as seen on watchOS 10



## Installation
Ready to use on iOS 17+ or watchOS 10+.

1. In Xcode, select **Add Packages…** from the File menu.
2. Enter `https://github.com/hiddevdploeg/ContentBlurView` in the search field.
3. Click **Add Package** (Set the Dependency Rule to Up to Next Major Version)
4. After adding the package, you will be able to import ContentBlurView in your project by using.

```swift
import ContentBlurView
```

## How use

You can use `ContentBlurView` with any `View` 

```swift
ContentBlurView {
    // Any view goes here
}
.ignoresSafeArea(edges: .all) // for fullscreen enjoyment

```
**Example with Map**

```swift

import MapKit
struct ContentView: View {
    var body: some View {
            ContentBlurView {
                Map(interactionModes: .rotate) {
                    Marker("Apple Park", coordinate: CLLocationCoordinate2D(latitude: 37.334268, longitude: -122.008715))
                }
                .mapStyle(.imagery)
            }
            .ignoresSafeArea(edges: .all)
    }
}

```

## Authors
This library is created by [Hidde van der Ploeg](https://hidde.design). Feel free to reach out on [Twitter](https://twitter.com/hiddevdploeg) or [Mastodon](https://mastodon.design/@hidde).

## License
ContentBlurView is available under the MIT license.


    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
    FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
    COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
    IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
    CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
