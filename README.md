# ContentBlurView
Easily get a fancy looking gradient blur as seen on watchOS 10

<img width="1242" alt="Example" src="https://github.com/hiddevdploeg/ContentBlurView/assets/5016984/60ad2220-f157-4310-bd13-319bc43b8b21">


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

### Directions
You can decide on which side the blur should start: `.topBlur`, `.leadingBlur`, `trailingBlur` or `.bottomBlur`. the default is `.bottomBlur`

### Text
It's recommended to use [`HierarchicalShapeStyle`](https://developer.apple.com/documentation/swiftui/hierarchicalshapestyle) as a `.foregroundStyle` of your text as this will make it more vibrant with the background.


**Examples**

```swift

import MapKit
struct ContentView: View {
    var body: some View {
            TabView {

            // Example with image and blur on top
            ContentBlurView(direction: .topBlur) {
                AsyncImage(url: URL(string: "https://picsum.photos/800"))
            }
            .ignoresSafeArea(edges: .all)

            // Example with Map and text on top of it
            ZStack(alignment: .bottom) {
                ContentBlurView {
                    Map(interactionModes: .rotate) {
                        Marker("Apple Park", coordinate: CLLocationCoordinate2D(latitude: 37.334268, longitude: -122.008715))
                    }
                    .mapStyle(.imagery)
                }
                .ignoresSafeArea(edges: .all)
                Text("Apple Park")
                    .font(.headline)
                    .foregroundStyle(.primary)
                    .padding()
            }
        }
        .tabViewStyle(.verticalPage)
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
