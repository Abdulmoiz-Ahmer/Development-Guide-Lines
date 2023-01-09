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

Use camelCase for folder and non-component file names and PascalCase for component file names

```
src/utils/form.ts
src/hooks/useForm.ts
src/components/banners/edit/Form.tsx
```

**Attributes**

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

**Avoid default export**

```
// Bad, Default exports don’t associate any name with the item being exported, meaning that any name can be applied during import. This may give you a flexibility, but if multiple developers imports the same module with different names or even non descriptive name than it causes confusion.
export default MyComponent;

// Good, Named exports are explicit, forcing the consumer to import with the names the original author intended and removing any ambiguity.
export { MyComponent };
export const MyComponent = ...;
export type MyComponentType = ...;

```

**Use props with children**

```
import React, { PropsWithChildren } from "react";

type ComponentProps = {
  someProperty: string;
};

// Good
function Component({ someProperty, children }: PropsWithChildren<ComponentProps>) {
  // ...
}
```

**Separate functions from the JSX**

```
// Bad
<button
  onClick={() => {
    setState(!state);
    resetForm();
    reloadData();
  }}
/>


// Good
const handleButtonClick = () => {
  setState(!state);
  resetForm();
  reloadData();
}

<button onClick={handleButtonClick} />

```

**Avoid using indexes as key props**

```
// Bad
const List = () => {
  const list = ["item1", "item2", "item3"];

  return (
    <ul>
      {list.map((value, index) => {
        return <li key={index}>{value}</li>;
      })}
    </ul>
  );
};

// Good
const List = () => {
  const list = [
    { id: "111", value: "item1" },
    { id: "222", value: "item2" },
    { id: "333", value: "item3" }
  ];

  return (
    <ul>
      {list.map((item) => {
        return <li key={item.id}>{item.value}</li>;
      })}
    </ul>
  );
};
```
**Use Fragments over html elements**

```
// Bad
const ActionButtons = ({ text1, text2 }) => {
  return (
    <div>
      <button>{text1}</button>
      <button>{text2}</button>
    </div>
  );
};

// Good
const Button = ({ text1, text2 }) => {
  return (
    <React.Fragment>
      <button>{text1}</button>
      <button>{text2}</button>
    </React.Fragment>
  );
};
```

**Prefer destructuring properties**

```
// Bad
const Button = (props) => {
  return <button>{props.text}</button>;
};

// Good
const Button = (props) => {
  const { text } = props;

  return <button>{text}</button>;
};

// Good
const Button = ({ text }) => {
  return <button>{text}</button>;
};
```

**Separation of concerns**
Separating the business logic from the presentation (rendering) makes the components code more readable. Most of the time this is applicable for the page/screen/container components where you are about to use multiple hooks or useEffects. Then the final code starts to be huge enough to be unreadable.

**Custom hooks**
To separate the responsibilities first of all you should create custom hooks instead of just putting a useEffect or multiple useStates directly to your component.

```
// Bad
const ScreenDimensions = () => {
  const [windowSize, setWindowSize] = useState({
    width: undefined,
    height: undefined
  });

  useEffect(() => {
    function handleResize() {
      setWindowSize({
        width: window.innerWidth,
        height: window.innerHeight
      });
    }

    window.addEventListener("resize", handleResize);
    handleResize();
  
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return (
    <>
      <p>Current screen width: {windowSize.width}</p>
      <p>Current screen height: {windowSize.height}</p>
    </>
  );
};

// Good
const useWindowSize = () => {
  const [windowSize, setWindowSize] = useState({
    width: undefined,
    height: undefined
  });

  useEffect(() => {
    function handleResize() {
      setWindowSize({
        width: window.innerWidth,
        height: window.innerHeight
      });
    }

    window.addEventListener("resize", handleResize);
    handleResize();

    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return windowSize;
};

const ScreenDimensions = () => {
  const windowSize = useWindowSize();

  return (
    <>
      <p>Current screen width: {windowSize.width}</p>
      <p>Current screen height: {windowSize.height}</p>
    </>
  );
};

```

Avoid huge components
Whenever it is possible, split your component into smaller chunks. Often applicable when you are using conditional rendering or defining the columns for a data grid, etc. Also applicable when a lot of custom hooks are used — check the section above.

```
// Bad
const SomeSection = ({ isEditable, value }) => {
  if (isEditable) {
    return (
      <Section>
        <Title>Edit this content</Title>
        <Content>{value}</Content>
        <Button>Clear content</Button>
      </Section>
    );
  }

  return (
    <Section>
      <Title>Read this content</Title>
      <Content>{value}</Content>
    </Section>
  );
};

// Good
const EditableSection = ({ value }) => {
  return (
    <Section>
      <Title>Edit this content</Title>
      <Content>{value}</Content>
      <Button>Clear content</Button>
    </Section>
  );
};

const DetailSection = ({ value }) => {
  return (
    <Section>
      <Title>Read this content</Title>
      <Content>{value}</Content>
    </Section>
  );
};

const SomeSection = ({ isEditable, value }) => {
  return isEditable ? (
    <EditableSection value={value} />
  ) : (
    <DetailSection value={value} />
  );
};

```

**Group the state whenever possible**

```
// Bad
const [username, setUsername] = useState('')
const [password, setPassword] = useState('')

// Good
const [user, setUser] = useState({})
```
If something can be derived from one state but can't be group with another state it shouldn't be state.

**Use shorthand for boolean props**

```
// Bad
<Form hasPadding={true} withError={true} />

// Good
<Form hasPadding withError />
```

**Avoid curly braces for string props**

```
// Bad
<Title variant={"h1"} value={"Home page"} />

// Good
<Title variant="h1" value="Home page" />
```

**Avoid using inline styles**
Ideally, use some third party for handling styles like CSS modules, JSS, styled-components, etc. or create a custom hook.

```
// Bad
const Title = (props) => {
  return (
    <h1 style={{ fontWeight: 600, fontSize: '24px' }} {...props}>
      {children}
    </h1>
  );
};

// Good
const useStyles = (props) => {
  return useMemo(
    () => ({
      header: { fontWeight: props.isBold ? 700 : 400, fontSize: "24px" }
    }),
    [props]
  );
};

const Title = (props) => {
  const styles = useStyles(props);

  return (
    <h1 style={styles.header} {...props}>
      {children}
    </h1>
  );
};
```

**Use constants or enums for string values**

```
// Bad
if (role === 'admin') {
  return <AdminUser />;
}

// Good
enum Roles {
  admin = 'admin',
  basic = 'basic',
}

if (role === Roles.admin) {
  return <AdminUser />;
}
```

**Don’t use third-party libraries directly**

Instead of importing the third-party libraries directly, re-export them in one centralised place.
```
src/lib/store.ts

export { useDispatch, useSelector } from 'react-redux';

src/lib/query.ts

export { useQuery, useMutation, useQueryClient } from 'react-query';
```
**Rely on abstraction instead of the implementation**
```
// Bad directly using momemt
import moment from 'moment';

const updateProduct = (product) => {
  const payload = {
    ...product,
    // Bad we are bound to the moment interface implementation
    updatedAt: moment().toDate(),
  };

  return await fetch(`/product/${product.id}`, {
    method: 'PUT',
    body: JSON.stringify(payload),
  });
};

// Good creating the abstraction, a.k.a. helper function which wraps the functionality

// utils/createDate.ts
import moment from 'moment';

export const createDate = (): Date => moment().toDate();

// updateProduct.ts
import { createDate } from './utils/createDate';

const updateProduct = (product) => {
  const payload = {
    ...product,
    // Good using the abstracted helper function
    updatedAt: createDate(),
  };

  return await fetch(`/product/${product.id}`, {
    method: 'PUT',
    body: JSON.stringify(payload),
  });
};
```
**Prefer declarative programming**
// Bad imperative: dealing with internals of array iteration
```
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
let sum = 0;

for (let i = 0; i < arr.length; i++) {
  sum += arr[i];
}
```

// Good declarative: we don't deal with internals of iteration
```
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const sum = arr.reduce((acc, v) => acc + v, 0);
```

**Use descriptive variable names**

```
// Bad Avoid single letter names
const n = 'Max';
// Good
const name = 'Max';

// Bad Avoid abbreviations
const sof = 'Sunday';
// Good
const startOfWeek = 'Sunday';

// Bad Avoid meaningless names
const foo = false;
// Good
const appInit = false;
```

**Avoid long list of function arguments**

```
// Bad
function createPerson(firstName, lastName, height, weight, gender) {
  // ...
}

// Good
function createPerson({ firstName, lastName, height, weight, gender }) {
  // ...
}

// Good
function createPerson(person) {
  const { firstName, lastName, height, weight, gender } = person;
  // ...
}
```

**Use object destructuring**
```

// ❌
return (
  <>
    <div> {user.name} </div>
    <div> {user.age} </div>
    <div> {user.profession} </div>
  </>  
)

// ✅
const { name, age, profession } = user;

return (
  <>
    <div> {name} </div>
    <div> {age} </div>
    <div> {profession} </div>
  </>  
)
```

**Prefer using template literals**
```

// Bad
const userName = user.firstName + " " + user.lastName;

// Good
const userDetails = `${user.firstName} ${user.lastName}`;
```

**Use implicit return in small functions**
```
// Bad
const add = (a, b) => {
  return a + b;
}

// Good
const add = (a, b) => a + b;
```
