const babelify = require('babelify');
const browserify = require('browserify');
const browserSync = require('browser-sync');
const cleanCSS = require('gulp-clean-css');
const concat = require('gulp-concat');
const del = require('del');
const gulp = require('gulp');
const imagemin = require('gulp-imagemin');
const jshint = require('gulp-jshint');
const lib = require('bower-files') ();
const source = require('vinyl-source-stream');
const uglify = require('gulp-uglify');
const utilities = require('gulp-util');

const buildProduction = utilities.env.prod; // append tag '--prod' to gulp command

gulp.task('jshint', () => {
  return gulp.src(['assets/js/*.js', 'spec/*-spec.js'])
    .pipe(jshint())
    .pipe(jshint.reporter('default'));
});

gulp.task('concatJS', () => {
  return gulp.src(['assets/js/*-interface.js'])
    .pipe(concat('allConcat.js'))
    .pipe(gulp.dest('tmp'));
});

gulp.task('twCSS', () => {
  const postcss = require('gulp-postcss');
  const tailwindcss = require('tailwindcss');

  return gulp.src('assets/css/tailwind.css')
    .pipe(postcss([
      tailwindcss('tailwind.js'),
      require('autoprefixer'),
    ]))
    .pipe(gulp.dest('tmp'));
});

gulp.task('concatCSS', ['twCSS'], () => {
    return gulp.src(['tmp/*.css'])
      .pipe(concat('vendor.min.css'))  // Change to allConcat after browserify issue is solved
      .pipe(gulp.dest('tmp'));
});

gulp.task('images', () => {
  gulp.src('assets/images/*')
    .pipe(gulp.dest('build/assets/images'));
});

gulp.task('jsBrowserify', ['concatJS'], () => {
  return browserify({ entries: ['tmp/allConcat.js'] })
    .transform(babelify.configure({
      presets: ["env"]
    }))
    .bundle()
    .pipe(source('app.js'))
    .pipe(gulp.dest('build/assets/js'));
});

gulp.task('cssBrowserify', ['concatCSS' , 'cleanCSS'], () => { // Gulp Error when using Browserify *look into browserify-css
  return gulp.src(['tmp/vendor.min.css', 'assets/css/app.css'])
    .pipe(gulp.dest('build/assets/css'));
});

gulp.task('minifyJS', ['jsBrowserify'], () => {
  return gulp.src('build/assets/js/app.js')
    .pipe(uglify())
    .pipe(gulp.dest('build/assets/js'));
});

gulp.task('minifyCSS', ['cssBrowserify'], () => {
  return gulp.src('build/assets/css/*.css')
    .pipe(cleanCSS({debug: true}, (details) => {
      console.log(`${details.name}: ${details.stats.originalSize}`);
      console.log(`${details.name}: ${details.stats.minifiedSize}`);
    }))
  .pipe(gulp.dest('build/assets/css'));
});

gulp.task('minifyImages', () => {
	gulp.src('assets/images/*')
		.pipe(imagemin())
		.pipe(gulp.dest('build/assets/images'))
});

gulp.task('jsBower', () => {
  return gulp.src(lib.ext('js').files)
    .pipe(concat('vendor.min.js'))
    .pipe(uglify())
    .pipe(gulp.dest('build/assets/js'));
});

gulp.task('bower', ['jsBower']);

gulp.task('clean', () => {
  return del(['build', 'tmp']);
});

gulp.task('cleanCSS', () => {
  return del(['tmp/*.css', '!tmp']);
});

gulp.task('build', ['clean'], () => {
  if (buildProduction) {
    gulp.start('minifyJS');
    gulp.start('minifyCSS');
    gulp.start('minifyImages');
  } else {
    gulp.start('jsBrowserify');
    gulp.start('cssBrowserify');
    gulp.start('images');
  }
});

gulp.task('serve', ['build'], () => {
  browserSync.init({
    server: {
      baseDir: "./",
      index: "index.html"
    }
  });

  gulp.watch(['assets/js/*.js'], ['jsBuild']); // Run jsBuild if any changes are made to any files with ext .js
  gulp.watch(['assets/css/*.css'], ['cssBuild']); // Run cssBuild if any changes are made to any files with ext .css
  gulp.watch(['bower.json'], ['bowerBuild']); // Run bowerBuild if any changes are made to our bower.json file
  gulp.watch(['*.html'], ['htmlBuild']); // Run htmlBuil if any changes are made to any files with ext .html
});

gulp.task('jsBuild', ['jsBrowserify', 'jshint'], () => {
  browserSync.reload();
});

if (buildProduction) {
  gulp.task('cssBuild', ['minifyCSS'], () => {
      browserSync.reload();
  });
} else {
  gulp.task('cssBuild', ['cssBrowserify'], () => {
      browserSync.reload();
  });
}

gulp.task('bowerBuild', ['bower'], () => {
  browserSync.reload();
});

gulp.task('htmlBuild', () => {
  browserSync.reload();
});
