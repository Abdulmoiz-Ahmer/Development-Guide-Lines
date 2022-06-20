# Development-Guide-Lines

**ReactJs**


There are several resources available to learn about React:

- [React documentation](https://reactjs.org/docs/getting-started.html)

- [Online courses](https://reactjs.org/community/courses.html)

**Components**

Component names should be descriptive and should not conflict with HTML element names in order to avoid confusion.

```
// Good
<SubmitButton/>

// Bad
<Button/>
```

```
**
Attributes**

Object literals should be stored as variables before being passed to an attribute to avoid double braces ({{ }}), avoid overly long lines, and make our code easier to read.

```
// Good
const styleList = {
  background: violet,
  color: yellow
};

const header = <h1 style={styleList}>Headline</h1>;

// Bad
const header = <h1 style={{background: violet, color: yellow}}>Headline</h1>;
```

**Event Handlers**

Naming of event handlers should follow a standard pattern using on and handle. The attribute name must be the word on with the name of the event and the method or function must be the word handle followed by the name of the event.

```
// Good
<SubmitButton onClick={handleClick}/>
<ContactForm onSubmit={handleSubmit}/>
<ExternalLink onHover={handleHover}/>

// Bad
<SubmitButton onClick={click}/>
<ContactForm onsubmit={submitForm}/>
<ExternalLink hover={changeColor}/>
```

**Fragments**

For better readability, prefer the long syntax to the short syntax.

```
// Good
class Layout extends Component{
  render(){
    return (
      <React.Fragment>
        <Header/>
        <Body/>
        <Footer/>
      <React.Fragment/>
    );
  }
}

// Bad
class Layout extends Component{
  render(){
    return (
      <>
        <Header/>
        <Body/>
        <Footer/>
      </>
    );
  }
}
```

**Presentational vs. Logical Components**

In a traditional MVC framework logic is kept from the View by way of Controllers. Data is kept separate from both by way of Models. This concept can be preserved by breaking components into components that specifically handle the “view” and containing components that handle the logic with the database layer handled by separate service functions and classes. 


**Types**

PropTypes should be specified for all applicable components

**Ternary Operators**

In general ternary operators are to be avoided in components though may be used in instances where the JSX within them can be written clearly on a single line.

```
// Good, it is simple to reason what markup is used in what situation
class BlogPost extends React.Component {
	// ...

	render() {
		// ...
	
		if(loading){
			return (
				<div>
					<figure className="loader">
						<img src="../loader.svg" alt=""></img>
					</figure>
				</div>
			);
		}
	
		return (
			<article>
				<header>
					<h2>{article.title}</h2>
					<time>{article.publish_date}</time>
					<p>{article.categories.join(', ')}</p>
				</header>
				<section>{article.content}</section>
			</article>
		);
	}
}

// Good, we've extracted all markup to individual components making the ternary logic simple to reason 
class BlogPost extends React.Component {
	// ...

	render() {
		// ...
	
		return loading ? <Spinner/> : <BlogPostContent/>;
	}
}

// Bad, the logic is hard to read and follow within multiple lines of markup
class BlogPost extends React.Component {
	// ...

	render() {
		// ...
		
		return (
			<React.Fragment>
				{loading ? (
					<div>
						<figure className="loader">
							<img src="../loader.svg" alt=""></img>
						</figure>
					</div>
				) : (
					<article>
						<header>
							<h2>{article.title}</h2>
							<time>{article.publish_date}</time>
							<p>{article.categories.join(', ')}</p>
						</header>
						<section>{article.content}</section>
					</article>
				)}
			</React.Fragment>
		);
	}
}
```


