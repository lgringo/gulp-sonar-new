# gulp-sonar

Sonar for gulp with updated dependencies to fix older lodash vulnerabilities caused by gulp-util.

## Install

```
npm install --save-dev gulp-sonar-new
```

## Usage Example

```js
gulp.task('sonar', function () {
    var options = {
        sonar: {
            host: {
                url: 'http://localhost:9000'
            },
            jdbc: {
                url: 'jdbc:mysql://localhost:3306/sonar',
                username: 'sonar',
                password: 'sonar'
            },
            projectKey: 'sonar:my-project:1.0.0',
            projectName: 'My Project',
            projectVersion: '1.0.0',
            // comma-delimited string of source directories
            sources: 'src/app/js,src/libs/js',
            language: 'js',
            sourceEncoding: 'UTF-8',
            javascript: {
                lcov: {
                    reportPath: 'test/sonar_report/lcov.info'
                }
            },
            exec: {
                // All these properties will be send to the child_process.exec method (see: https://nodejs.org/api/child_process.html#child_process_child_process_exec_command_options_callback )
                // Increase the amount of data allowed on stdout or stderr (if this value is exceeded then the child process is killed, and the gulp-sonar will fail).
                maxBuffer : 1024*1024
            }
        }
    };

    // gulp source doesn't matter, all files are referenced in options object above
    return gulp.src('thisFileDoesNotExist.js', { read: false })
        .pipe(sonar(options))
        .on('error', util.log);
});
```

## Credit

Inspired by [grunt-sonar-runner](https://github.com/skhatri/grunt-sonar-runner) by [Suresh Khatri](https://github.com/skhatri).
Forked from [gulp-sonar](https://github.com/carsdotcom/gulp-sonar) by [carsdotcom](https://github.com/carsdotcom)
Thanks to [Floix](https://github.com/Floix) for providing the changes in a fork on the original branch.