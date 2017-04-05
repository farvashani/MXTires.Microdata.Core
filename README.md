# MXTires.Microdata.Core

## ORIGINAL README
NET Core 1.1.1 version of MXTires.Microdata.

Removed from original version references for System.Web and changed Assembly instance in MXTires.Microdata.Core.Validators class.

MXTires.Microdata is framework to correspond schema.org object types to .Net classes with conversion to JSON


## Code before:

Assembly asm = Assembly.GetExecutingAssembly();

## Code after:

Assembly asm = System.Reflection.Assembly.GetEntryAssembly();

## Visual Studio 2017 tested



## Prerequisites
Newtonsoft.Json
[NuGet](https://www.nuget.org/packages/Newtonsoft.Json "NuGet")

## Code example of defining a Product:
[https://schema.org/Product](https://schema.org/Product/ "Product")
```
        public void SimpleProduct()
        {
            var product = new Product()
            {
                Name = "T3 REPLICA NISSAN ALTIMA, MAXIMA (PAINTED/SILVER)",
            };
            Review review1 = new Review() { Name = "Review1", ReviewRating = new Rating() { RatingValue = "5" }, ReviewBody = "Best product ever!", Author = new Person() { Name = "Some Guy" } };
            Review review2 = new Review() { Name = "Review2",  ReviewRating = new Rating() { RatingValue = "4" }, ReviewBody = "I've seen better...", Author = new Person() { Name = "Other Guy" } };
            product.Reviews = new List<Review> { review1, review2 };
            System.Diagnostics.Debug.Write(product.ToJson());
        }
```

## Code example of defining an Event:
[https://schema.org/Event](https://schema.org/Event/ "Event")
```
        public void EventTest()
        {
            var baseEvent = new Event();
            baseEvent.Attendee = new Person();
            System.Diagnostics.Debug.WriteLine(baseEvent.ToIndentedJson());
        
        }
```
## Code example for image:
```
        [TestMethod]
        public void TestImageObject()
        {
            var blogPosting = new BlogPosting();
            blogPosting.Image = new ImageObject()
            {
                Url = "http://whatever.com/image.png",
                Width = new QuantitativeValue() { Value = 500 },
                Height = new QuantitativeValue() { Value = 500 }
            };

            System.Diagnostics.Debug.Write(blogPosting.ToIndentedJson());
        }
```
### Output:
```
<script type="application/ld+json">{
  "image": {
    "height": {
      "value": 500.0,
      "@context": "http://schema.org",
      "@type": "QuantitativeValue"
    },
    "width": {
      "value": 500.0,
      "@context": "http://schema.org",
      "@type": "QuantitativeValue"
    },
    "url": "http://whatever.com/image.png",
    "@context": "http://schema.org",
    "@type": "ImageObject"
  },
  "@context": "http://schema.org",
  "@type": "BlogPosting"
}</script>
```

## Code example with extentions:
```
        public void TestAtlas()
        {
            var atlas = new Atlas();
            atlas.Context = new List<object>() { "http://schema.org", new Extentions.BibNameSpace(), };
            atlas.Name = "Atlas of the world.";
            System.Diagnostics.Debug.WriteLine(atlas.ToIndentedJson());
        }
```
### Output:
```
<script type="application/ld+json">{
  "name": "Atlas of the world.",
  "@context": [
    "http://schema.org",
    {
      "bib": "http://bib.schema.org"
    }
  ],
  "@type": "Atlas"
}</script>
```

## Dependencies
[Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/ "Newtonsoft.Json") (>= 7.0.0)



## License

[1010Tires.com](http://www.1010tires.com/). License - [License.md](https://github.com/idenys/MXTires.Microdata/blob/master/License.md)
