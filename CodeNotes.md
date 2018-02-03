# WillowTree code analysis

All line notes refer to the unedited version of the code, not the result of my refactoring and improvements.
### Add CSS
- Make the webpage wider from ```400px``` to ```600px```.
- Make logo same width as the app.
- Add a ```margin-top: 10px``` to the logo.
- Align table text to the center
- Add Background image of Charlottesville's Downtown Mall
- Add ```overflow-y: scroll;``` to the body CSS to fix scrollbar to screen and prevent jitters.

### Refactor to ES6
Remove code written in the ES5 style and update to ES6 standards.
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

### Improve Search Engine
#### Old Version (Line 165):
```
function filterByName(searchForName, personList) {
            return personList.filter((person) => {
                return person.firstName === searchForName || person.lastName === searchForName;
            });
        }
```
#### New Version
```
function filterByName(searchForName, personList) {
  let regex = new RegExp('^' + searchForName.toLowerCase());
    return personList.filter((person) => {
        return person.firstName.toLowerCase().match(regex) || person.lastName.toLowerCase().match(regex);
    });
}
```
- Add a new Regular Expression constructor and set it to create a regex object based on the lowercase search string at the beginning and any characters following.
- Refactor the filter function to return the lowercase first or last name matched to the regex of the search term.
- Result is a constantly updating search with all potential matches returned in real time.


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

## Create New Elements
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

### Add Title Field
```
const getTitle = person  => {
  if (person.jobTitle) {
    return person.jobTitle;
  } else {
    return "Cat Herder";
  };
};
/// break
React.DOM.th({ key: 'title-h' }, null, 'Title')
/// break
React.DOM.td({ key: 'title' }, null, getTitle(props.person))
```
- Add a job title field to the table.
- If no title, add title "Cat Herder".
