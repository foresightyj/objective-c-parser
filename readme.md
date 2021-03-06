# objective-c-parser [![Build Status](https://travis-ci.org/DanielMSchmidt/objective-c-parser.svg?branch=master)](https://travis-ci.org/DanielMSchmidt/objective-c-parser) [![Coverage Status](https://coveralls.io/repos/github/DanielMSchmidt/objective-c-parser/badge.svg?branch=master)](https://coveralls.io/github/DanielMSchmidt/objective-c-parser?branch=master) [![BCH compliance](https://bettercodehub.com/edge/badge/DanielMSchmidt/objective-c-parser?branch=master)](https://bettercodehub.com/)

> Get an objective-c header file and translate it to equivalent javascript calls


## Install

```
$ npm install objective-c-parser
```


## Usage

```js
const fs = require('fs');
const objectiveCParser = require('objective-c-parser');
const content = fs.readFileSync('/path/to/objective-c/Ponies.h')

const output = objectiveCParser(content);

fs.writeFileSync('/path/to/project/ponies.json', output);
```

## Example

```objective-c
#import <Foundation/Foundation.h>
@protocol Ponies, Foo;
@interface BasicName : NSObject

// Another stupid comment
@property(nonatomic, readonly) uninteresting<IgnorePlease> matcher;


// This is the comment of basic method one
- (NSInteger)basicMethodOne;

/**
 *  This is the comment of basic method two.
 *  It has multiple lines
 */
- (NSString) basicMethodTwoWithArgOne:(NSInteger)argOne AndArgTwo:(NSString)argTwo;
@end
```

```json
{
  "name": "BasicName",
  "methods": [
    {
      "args": [],
      "comment": "This is the comment of basic method one",
      "name": "basicMethodOne",
      "returnType": "NSInteger"
    },
    {
      "args": [
        {
          "type": "NSInteger",
          "name": "argOne"
        },
        {
          "type": "NSString",
          "name": "argTwo"
        }
      ],
      "comment": "This is the comment of basic method two.\nIt has multiple lines",
      "name": "basicMethodTwoWithArgOneAndArgTwo",
      "returnType": "NSString"
    }
  ]
}
```

## License

MIT © [Daniel Schmidt](http://danielmschmidt.de)
