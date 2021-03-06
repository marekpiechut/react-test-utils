React Test Utils
================

ReactTestUtils from facebook ReactTestUtils, export it as a single repo, just make it more easy to included in and testing your React components.

eg:

```js
/** @jsx React.DOM **/

var React = require('react/addons');
require('react-test-utils');
// or var ReactTestUtils = require('react-test-utils');
var test = require('tape');
var Player = require('../../js/Player');
var sinon = require('sinon');
var ReactTestUtils = React.addons.ReactTestUtils;

var onMusicAdd = sinon.spy();

test('Player', function(t) {
  var player = <Player test='testing' />;
  ReactTestUtils.renderIntoDocument(player);
  t.plan(1);
  t.equal(player.props.test, 'testing', 'test property should exists');
});

test('Player: simulate drag music', function(t) {
  var player = <Player test='testing' onMusicAdd={onMusicAdd}/>;
  var files = [
    {name: 'test.mp3', type: 'audio/mp3'}
  ];
  var fakeEvt = {
    dataTransfer: {
      files: files
    }
  };
  ReactTestUtils.renderIntoDocument(player);

  t.plan(3);

  ReactTestUtils.Simulate.drop(player.refs.el);
  t.notOk(onMusicAdd.called, 'onMusicAdd should not be called');

  ReactTestUtils.Simulate.drop(player.refs.el, fakeEvt);
  t.ok(onMusicAdd.called, 'onMusicAdd should be called');
  t.ok(onMusicAdd.calledWith(files), 'onMusicAdd shoule be called with mock files');
});

```

just copy the ReactTestUtils from the facebook/react project, :p it works!