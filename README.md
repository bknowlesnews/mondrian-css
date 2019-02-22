# mondrian-css
## Semantically manage assignment of functional CSS in code
> The primary objective of Mondrian CSS is to empower designers and engineers to
meaningfully group reusable collections of functional styles without impacting the
resulting functional CSS classes.

### mondrian-css Using Tachyons with React and TypeScript
#### Easy to set up
install from npm:
```
npm install --save mondrian-css
```
import mondrian-css into your code and pass some configuration to the init method:

```
import react, {FunctionComponent, useState} from "react";
import mcss from "mondrian-css";

//mondrian config can be imported from a JSON filen or declared inline

const _m = mcss.init({
    "strict":true,
    "styles":[ "../styles/tachyons.css" ],
    "default":{
        "special-section":"tc ph4"],
        "panel":"center mw5 mw6-ns hidden ba mv4",
        "list":"pa4"
    }
    "modern":{
        "panel":"enter mw5 mw6-ns hidden ba mv4 b--dotted shadow-5"
    },
    "antique":{
        "list":{  
            "extend":"default.list",
            "with":"bg-washed-yellow shadow-5 ba fw3"
        },
        "panel":"enter mw5 mw6-ns hidden bt mv4 b--dotted shadow-5"
    }
});
```
* Just declare your themes and semantic styles in the configuration object, referencing the classes from CSS as they would appear in the HTML class attribute.
* The default behaviour of mondrian-css is to look for a style group in the specified theme and then fall back to the default theme if nothing is found. These may occur when extending one style group from another.
* With strict mode enabled, whether you use mondrian-css during compilation or at runtime, it will warn of any style collisions during the init method.
#### Easy to write 
```
const [theme, setTheme] = useState("antique");

export interface MCProps{ data:string[] };

export const MyComponent:FunctionComponent<MCProps> = props =>(
    <ThemeSelector data={_m.themes} onChange={e=>setTheme(e.selectedItem)} theme={theme} />
    <section className={_m("special-section")}>
        <Panel title="mondrian-css example" className={_m("panel").t(theme)}>
            <List data={props.data} className={_m("list").t(theme)} />
        </Panel>
    <section/>
    
);
```
* It is entirely optional when and where you use mondrian-css to assign classes
* If you don't specify a theme mondrian-css will look for the default

#### The Resulting HTML and class assignment
```
<ThemeSelector theme="antique" > ... </ThemeSelector>
<section class="tc ph4">
    <Panel title="mondrian-css example" class="center mw5 mw6-ns hidden bt mv4 b--dotted shadow-5">
        <List class="pa4 bg-washed-yellow shadow-5 ba fw3"> ... </List>
    </Panel>
<section/>
```

* mondrian-css makes it easy to assign or change large groups of classes.
* It can help keep your HTML markup clean and implementation agnostic.

[~~Try it now!~~](https://github.com/bknowlesnews/mondrian-css/) ***coming soon***
