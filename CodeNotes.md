# WillowTree code analysis

All line notes refer to the unedited version of the code, not the result of my refactoring and improvements
### Update Images
#### Initial Code (Line 137):
```
const getImageUrl = (person) => {
            return `http:${person.headshot.url}`;
        };
```
#### New Version
```
const getImageUrl = (person) => {
    if (person.headshot.url) {
      return `http:${person.headshot.url}`;
    } else {
      return "http://images.contentful.com/3cttzl4i3k1h/5ZUiD3uOByWWuaSQsayAQ6/c630e7f851d5adb1876c118dc4811aed/featured-image-TEST1.png";
    }
};
```
Add a placeholder image to all persons in the API results if lacking one
