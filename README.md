# reactDarkMode
This React app creates a toggle dark mode for specified pages.

This React app utilizes moment.js, the data-formatting library: https://momentjs.com/

A general overview of the pertinent React code is provided below:

First the navbar is setup and the data ia mapped over to return all of the article components that exists inside of data.js.
```React
function App() {
  return (
    <main>
      <nav>
        <div className="nav-center">
          <h1>overreacted</h1>
          <button className="btn">toggle</button>
        </div>
      </nav>
      <section className="articles">
        {data.map((item) => {
          return <Article key={item.id} {...item} />;
        })}
      </section>
    </main>
  );
}
```

Next the article is worked upon using deconstruction on the data to display it on screen.
```React
const Article = ({ title, snippet, data, length }) => {
  console.log(date);

  return (
    <article className="post">
      <h2>{title}</h2>
      <div className="post-info">
        <span>date</span>
        <span>{length} min read</span>
      </div>
      <p>{snippet}</p>
    </article>
  );
};
```

Next momentJS is used to format the dates.
```React
        <span>{moment(date).format("dddd Do, YYYY")}</span>
```

Next the toggle functionality is addressed using changes to CSS.
```CSS
.dark-theme {
  --clr-bcg: #282c35;
  --clr-font: #fff;
  --clr-primary: yellow;
}
.light-theme {
  --clr-bcg: #fff;
  --clr-font: #282c35;
  --clr-primary: deepskyblue;
}
```

Next the button is set up to toggle the classes in App.js using useState with useEffect.
```React
function App() {
  const [theme, setTheme] = useState("light-theme");

  useEffect(() => {
    document.documentElement.className = theme;
  }, [theme]);
  return (.....
  
           <button className="btn" onClick={toggle}>toggle</button>
```

Next the toggle function was created.
```React
  const toggle = () => {
    if (theme === "light-theme") {
      setTheme("dark-theme");
    } else {
      setTheme("light-theme");
    }
  };
```

Last the user settings are saved into local storage to render correct settings upon page render.
```React
const getStorageTheme = () => {
  let theme = 'light-theme'
  if(localStorage.getItem('theme')){
    theme = localStorage.getItem('theme')
  }
  return theme;
};

function App() {
  const [theme, setTheme] = useState(getStorageTheme);
  
    useEffect(() => {
    document.documentElement.className = theme;
    localStorage.setItem("theme", theme);
  }, [theme]);
```


***End walkthrough
