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

It's as easy
```swift



```

Alternatively, you can customize the `BillboardView` and position it in any way that suits your app. This view takes a `BillboardAd`, a `BillboardConfiguration` (Optionally), and a view that represents your paywall:

```swift

@State private var advertisement: BillboardAd? = nil
@StateObject var viewModel = BillboardViewModel()


ContentView()
    .task {
        let newAdvert = try? await viewModel.fetchRandomAd()
        advertisement = newAdvert
    }
    .fullScreenCover(item: $advertisement) { advert in
        BillboardView(advert: advert, paywall: { Text("Paywall") })
    }

```

**TIP**: When you're running a debug version of your app you can tap on the timer to show a dismiss button right away.

![Examples@2x](https://github.com/hiddevdploeg/Billboard/assets/5016984/37901294-82cb-4586-8134-38496dbb33cc)


## BillboardBannerView

If you don't fancy a fullscreen view but prefer a smaller banner to display within your content you can do that now too! Simple add a `BillboardBannerView` wherever you like.

```swift
@State private var advert: BillboardAd? = nil
ContentView()
    .safeAreaInset(edge: .bottom) {
        if let advert {
            BillboardBannerView(advert: advert)
                .padding()
        }
    }
```

By default it comes with a shadow, which you can opt-out from by changing the `includeShadow` value. Here's an example on how you could include a `BillboardBannerView` in your list:

```swift
@State private var advert: BillboardAd? = nil

List {
    if let advert {
        Section {
            BillboardBannerView(advert: advert, includeShadow: false)
                .listRowBackground(Color.clear)
                .listRowInsets(.init(top: 0, leading: 0, bottom: 0, trailing: 0))
        }
    }
    
    // Rest of the list...
}

```

![BillboardBannerExamples](https://github.com/hiddevdploeg/Billboard/assets/5016984/259603dd-3160-4552-a3da-990ecb33afd4)

## Configuration

Billboard lets you define some configurations to fit your needs better.

``` swift
public struct BillboardConfiguration {
    
    /// The URL pointing to the JSON in the `BillboardAdResponse` format.
    public let adsJSONURL: URL?
    
    /// Enable or disable haptics
    public let allowHaptics: Bool
    
    /// The duration of the advertisement
    public let duration: TimeInterval
    
    /// Provide a list of Apple ID's that you want to exclude from showing up (e.g. your own app)
    public let excludedIDs : [String]
    
    public init(adsJSONURL: URL? = URL(string:"https://billboard-source.vercel.app/ads.json"),
                allowHaptics: Bool = true,
                advertDuration: TimeInterval = 15.0, excludedIDs: [String] = []) {
        self.adsJSONURL = adsJSONURL
        self.allowHaptics = allowHaptics
        self.duration = advertDuration
        self.excludedIDs = excludedIDs
    }
}
```

This also allows you to use your own source of ads that follow the `BillboardAdResponse` format.

```swift

@State private var showRandomAdvert = false

let config = BillboardConfiguration(
    adsJSONURL: URL(string: "YOUR-OWN-SOURCE"),
    allowHaptics: false,
    advertDuration: 30.0,
    excludedIDs: ["1234567890"]
)

ContentView()
    .showBillboard(when: $showRandomAdvert, configuration: config) {
        // Replace this view with your Paywall
        Text("Your Paywall goes here")
    }

```


## BillboardAdResponse
Here's an example of how your source list could look like.

```json
{
  "ads" : [
    {
      "appStoreID" : "1574243765",
      "name" : "NowPlaying",
      "title": "Learn everything about any song",
      "description" : "A music companion app that lets you discover the stories behind and song, album or artist.",
      "media": "https://pub-378e0dd96b5343108a04317ebddebb4e.r2.dev/nowplaying.png",
      "backgroundColor" : "344442",
      "textColor" : "EFDED7",
      "tintColor" : "EFDED7",
      "fullscreen": false,
      "transparent": true
    }
  ]
}

```

![Ad Example@2x](https://github.com/hiddevdploeg/Billboard/assets/5016984/0351d110-1f51-45ab-9d61-497d87653dfa)


## Ad Guidelines & Requirements
Submit your app to be featured as an Ad for everyone using the Billboard package to display Advertisements.
Each ad will be reviewed before inclusion.

**[You can submit your app here](https://forms.gle/nWV4dT3taBF62WXbA)**

Feel free to use the [Billboard template for Figma](https://www.figma.com/community/file/1257700620161188779) to tweak and preview the promo.

### Ad Requirements
- **Apple ID of App**: The Apple ID is a 9- or 10-digit number found in your App Store URL or in App Store Connect.
- **Name of App**: The name of the app you're promoting
- **Title**: The advertisement headline (maximum 25 characters).
- **Description**: The advertisement description (maximum 140 characters).
- **Media**: The image used in your advertisement.

### Media Guidelines
- Image should be a minimum of 1280x1280 in resolution.
- The image should not contain any text outside of the visual content.
- Avoid using your App Icon as the image (as it's already displayed by default).
- Provide an image with no background or has a single color (avoid gradients).
- Photos are allowed as well but will be displayed differently.

## Ad Types
The media of an ad will be displayed covering the whole view when `BillboardAd.fullscreen` is set to `true`. This works great if the media is a photo instead of a visual. Please consider that the photo's subject must be in the center, which will ensure it's always visible.

![AdTypes@2x](https://github.com/hiddevdploeg/Billboard/assets/5016984/c7e2f96a-6368-4807-9c81-7dddd008d5ad)



## FAQ
### Which Ads are presented when I use the default config
You'll find a list of all currently used ads in the example app.

## Special thanks to
[tundsdev](https://twitter.com/tundsdev) for CachedImage implementation

## Authors
This library is created by [Hidde van der Ploeg](https://hidde.design). Feel free to reach out on [Twitter](https://twitter.com/hiddevdploeg) or [Mastodon](https://mastodon.design/@hidde).

## License
Billboard is available under the MIT license.


    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
    FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
    COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
    IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
    CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
