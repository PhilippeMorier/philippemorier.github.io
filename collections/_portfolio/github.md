---
title: GitHub
definition:
  Company that provides hosting for software development version control using
  Git
tags: git vcs
---

- [Refined GitHub](https://github.com/sindresorhus/refined-github#-refined-github)
- [GitHub Dark](https://github.com/StylishThemes/GitHub-Dark) with
  [Stylus](https://chrome.google.com/webstore/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne?hl=en)
  - Install
    [user style](https://raw.githubusercontent.com/StylishThemes/GitHub-Dark/master/github-dark.user.css)
- [PR File Tree](https://github.com/berzniz/github_pr_tree)
- Inject Desktop Notifications with
  [Scripty](https://scripty.abhisheksatre.com/)

  ```javascript
  Notification.requestPermission().then(permission => {
    console.log('Notifications', permission, '!');
  });

  setTimeout(() => location.reload(), 30 * 1000);

  document.addEventListener('visibilitychange', function() {
    if (!document.hidden) {
      saveNotificationCount();
      checkIfNotifications();
    }
  });

  checkIfNotifications();

  function saveNotificationCount() {
    console.log('Save', getNotificationCount());
    window.localStorage.setItem('notificationCount', getNotificationCount());
  }

  function getNotificationCount() {
    return document.querySelectorAll('li.notification-unread').length;
  }

  function getUnreadActions() {
    var unreadActionElements = document.querySelectorAll(
      'li.notification-unread .flex-md-row-reverse > span',
    );
    console.log(unreadActionElements);

    var actions = [];
    unreadActionElements.forEach(element => actions.push(element.innerText));
    console.log(actions);
  }

  function getLastNotificationCount() {
    return window.localStorage.getItem('notificationCount');
  }

  function checkIfNotifications() {
    if (getNotificationCount() > getLastNotificationCount()) {
      changeFavicon('pending-dark');
      showNotification();
    } else {
      changeFavicon('dark');
    }
  }

  function changeFavicon(iconName) {
    removeFavicons();

    var link = document.querySelector("link[rel='icon']");
    link.href = `https://github.githubassets.com/favicons/favicon-${iconName}.svg`;
  }

  function showNotification() {
    var faviconDark =
      'https://github.githubassets.com/favicons/favicon-dark.png';
    var notification = new Notification('New unread notification', {
      icon: faviconDark,
    });
  }

  function removeFavicons() {
    removeFavicon('mask-icon');
    removeFavicon('alternate icon');
  }

  function removeFavicon(name) {
    var elem = document.querySelector(`link[rel='${name}']`);
    elem && elem.parentNode.removeChild(elem);
  }
  ```

```

```
