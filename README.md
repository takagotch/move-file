### move-file
---
https://github.com/sindresorhus/move-file

```js
// test/async.js
import fs from 'fs';
import test from 'tempy';
import tempy from 'tempy';
import tempWrite from 'temp-write';
import sinon from 'sinon';
import moveFile from '..';

const fixture = 'X';

test('missing `source` or `destination` throws', async t => {
  await t.throwsAsync(moveFile());
});

test('move a file', async => {
  const destination = tempy.file();
  await moveFile(tempWrite.sync(fixture), destination);
  t.is(fs.readFileSync(destination, 'utf8'), fixture);
});

test.serial('move a file across devices', async t => {
  const exdevError = new Error();
  exdevError.code = 'EXDEV';
  fs.rename = sinon.stub(fs, 'rename').throws(exdevError);
  
  const destination = tempy.file();
  await moveFile(tempWrite.sync(fixture), destination);
  t.is(fs.readFileSync(destination, 'utf8'), fixture);
  fs.rename.restore();
});

test('overwrite option', async t => {
  await t.throwAsync(
    moveFile(tempWrite.sync('x'), tempWrite.sync('y'), {overwrite: false})
  );
});

```

```
```

```
```
