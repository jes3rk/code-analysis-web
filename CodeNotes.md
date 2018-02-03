# WillowTree code analysis

All line notes refer to the unedited version of the code, not the result of my refactoring and improvements.
### Add CSS
- Make the webpage wider from ```400px``` to ```500px```.
- Make logo same width as the app.
- Add a ```margin-top: 10px``` to the logo.

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
Add a placeholder image to all persons in the API results if lacking one.

### Sort by Last Name
#### Initial Code (Line 211):
```
const sortByLastName = (personList) => sortByFirstName(personList).reverse();
```
#### New Version
```
const sortByLastName = sortObjListByProp('lastName');
```
Sort the employee list by last name rather than just reversing the first name sort.

## Create New Elements in Primary render
### Add Logo
```
React.DOM.img({ key: 'logo', alt: 'WillowTree Logo', src: 'https://skilled.co/wp-content/uploads/2017/01/Willow-Tree-Apps.png', className: 'logo'})
```
Add the company logo to the top of the page and add CSS to fit it to the app container.

### Add Subtitle
```
React.DOM.h2({ key: 'subtitle' }, null, 'Company Directory')
```
Add a subtitle to specifically refer to the company directory.
