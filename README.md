# Boilerplate Javascript NPM/Gulp/Karma Generator

This bash script takes the headache that is setting up a JS project with npm/gulp/etc..etc.. and automates that process. It keeps you informed on exactly what it is doing when it's doing via terminal messages.

After the script is done generating the boilerplate project, it will run gulp jshint to make sure there are no syntactical errors. Then it will run gulp build --prod to make sure all gulp tasks are working properly. Finally it will run npm test just to verify that karma-jasmine was setup correctly.


## Setup/Installation Requirements

* Clone this repo. <br />
`$ git clone https://github.com/AbdulYahya/gulp-boilerplate-gen.git`
* cd into the cloned repo and run the following command from your terminal. <br />
`$ ./generate`
* Follow the command prompts

## License

[MIT License][Arbitrary case-insensitive reference text]

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

###### Copyright (c) 2018 Abdullah Yahya

[arbitrary case-insensitive reference text]: https://ayahya.mit-license.org
