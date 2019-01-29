# Shallow Props

**Not ideal**

```jsx
// App.js
// data = {
//   id: '12kd9v11',
//   name: 'Homer',
//   jobTitle: 'Safety Inspector',
//   company: 'Springfield Nuclear Power Plant',
//   catchPhrase: 'Doh!'
// }

<div>
  <Simpson data={data} />
</div>
```

**Better!**

```jsx
// App.js
<div>
  <Simpson
    id='12kd9v11'
    name='Homer'
    jobTitle='Safety Inspector'
    company='Springfield Nuclear Power Plant'
    catchPhrase='Doh!'
  />
</div>
```

...or

```jsx
// App.js
const data = {
  id: '12kd9v11',
  name: 'Homer',
  jobTitle: 'Safety Inspector',
  company: 'Springfield Nuclear Power Plant',
  catchPhrase: 'Doh!'
}

<div>
  <Simpson {...data} />
</div>
```