# WebView Event Posting App

This is a simple web application designed to emit events to a Flutter mobile application via WebView. It uses `window.postMessage` and `FlutterChannel.postMessage` to send messages like `app_success` and `consent_granted`.

## Overview

The app allows external communication with host apps (e.g., Flutter apps embedding it via WebView) to notify them about user actions.

## Live Demo

[https://web-app-with-event-posting.web.app](https://web-app-with-event-posting.web.app)

## Event Emission Logic

```html
<script>
  function emitSuccess() {
    if (window.parent !== window) {
      window.parent.postMessage('app_success', '*');
    } else if (window.FlutterChannel) {
      FlutterChannel.postMessage('app_success');
    }
  }

  function emitConsent() {
    if (window.parent !== window) {
      window.parent.postMessage('consent_granted', '*');
    } else if (window.FlutterChannel) {
      FlutterChannel.postMessage('consent_granted');
    }
  }

  window.onload = () => {
    document.getElementById("btn-success").addEventListener("click", emitSuccess);
    document.getElementById("btn-consent").addEventListener("click", emitConsent);
  };
</script>
