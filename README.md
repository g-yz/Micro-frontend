### Key Concepts

`Microfronts` `Frontend` `ReactJs` `Àngular`

### Contents

1. [Goals](#goals) 
   
2. [Research](#research)

    2.1. [Overview](#overview)

    2.2. [Microfront](#microfront)

    2.3. [Technological options](#technological-options)

    2.4. [Approaches using module federation](#approaches-using-module-federation)

    2.5. [Experiments](#experiments)

    2.6. [Implementation effort](#implementation-effort)

  
3. [Conclusion](#conclusion)

4. [References](#references)

## Goals

Investigate if it is possible to imbibe the map board developed by ReactJS technology into a Angular technology project:

- Focus in the micro frontend technologies in order to define if it is possible to imbibe the map board with ReactJS into the Meetpoint project which is implemented with Angular.

- Create a small project to prove this concept.

- Make sure that we could interact between both technologies successfully. We would need to send some values between them.

- Contemplate the time cost of the functionality of the embedded functionality. Make sure that the all flow is gonna work fluently.

- Contemplate the cost of implement it. (optional)

## Research

### Overview

After the great success of the Microservices architecture around 2011, Thought Works added to the technology radar the term "Microfrontends" for the first time in Nov 2016, as a frontend architecture similar to microservices for frontend development. This architectural design came because of the monolith microcontent with Single Page Applications that created similar challenges to the backend monolith architecture. after that, companies started to implement frameworks that could help build frontends using this new architecture. 

In November 2017, Thought Works recommended Single-Spa for Microfrontends implementation. But by the end of 2020, Jack Jackson released his masterpiece "Module Federation" as a plugin in Webpack 5. The Module Federation Plugin changed the world of Microfrontends to a totally new level. Now, it's posible include a remote component to our project as we have developed it locally without depending on the build or deployment or even having a web server to run it. 
Finally, around April 2021, Thoughtworks started to recommend Module Federation for Microfrontends implementations.
However, micro frontends are still in their early steps since there are still several aspects to review like segurity, intercommunication, etc.

![image](https://user-images.githubusercontent.com/12683240/214583851-9b6557ec-1784-4e07-ae8e-6f3bd71bcc8f.png)

### Microfront

Micro Frontends are designed to break down the frontend monolith into smaller, more manageable chunks. Each team can own its features from start to finish, develop in its codebase, release versions independently, offer minor incremental upgrades regularly, and interface with other teams to compose and manage pages and applications together. 

Benefits

1) Increases autonomy of independent teams: Micro-frontends are great tools for helping teams work autonomously by dividing teams first and code second. Each team has complete control over a vertical slice of the programme and can specialise in their field. They won't have to worry as much about unintentional interference from other teams, and they won't have to coordinate as much.  

2) Eases organisation of code and artefacts: Micro-frontends, in principle, can help you enhance the structure of your codebase by containing a smaller, concentrated section of the application in each micro-frontend. It's a common misconception that monolithic apps can't be adequately structured; in fact, a few minor tweaks can provide one with just as many benefits as totally dividing your application.  

3) Eases the deployment process: One has the opportunity to distribute pieces of your frontend independently with micro-frontends. You can merely deploy what has changed rather than redeploying everything. You can also give teams the freedom to release whenever they choose, without having tocoordinate with other teams or adhere to a company-wide release cycle. You can undo a faulty release without harming other teams' work.  

4) Multiple technical choices: The last widely stated advantage of micro-frontends is that it allows everyone to use a variety of frontend frameworks and technologies. While a small team is unlikely to wish to learn and use numerous frontends at the same time, it does provide an upgrade route when it comes to future tools and frameworks.  
Instead of needing all teams to coordinate updates, micro-frontends allow each team to upgrade their technology stack separately. Supporting several tech stacks also makes it easy to include off-the-shelf solutions, independent of the framework.  


Common issues of Micro Frontend

1) Sharing a common function: The multi-repo strategy employs numerous repositories to house the services of a company's project. It’s tough to share libraries across multiple repos. It involves uploading artefacts to a package registry, where repos define a version range as a dependency. Worse, shared code usually has its repository, which necessitates creating build tools, unit testing, and continuous integration. Inheriting changes to shared code necessitates changing the package's dependence, which is a headache in and of itself.  

2) Managing application-wide changes: Making a change across numerous micro frontends necessitates altering multiple repositories when micro frontends are split up into distinct repositories. This means that a commit must land in each repository, and different teams' releases may need to be synchronised. Even if the change's code is housed within a common package, each repository must still update the dependency's version.  

### Technological options

#### Iframe

The iFrame provides a sandboxing behaviour with a decent level of isolation and can even load content across domain. iFrames that exist under the same domain can access the browser storage (such as localStorage and sessionStorage) with values set by the web app shell or other Micro Frontend.

In the scenario you may need to display the server-rendered UI from the legacy web application built with .php, .jsp, and/or .asp. It also needs to co-exist with the new client-rendered Micro Frontend built with the modern JavaScript framework. The iFrame would help with loading and rendering the server-rendered HTML, while the other parts of page are client-side rendered.

Despite the usefulness of iFrame, it does come with some downsides:

- Top-level routing cannot be propagated to the iFrame page without extra work
- Challenging to synchronize with browser history, deep linking with bookmark use cases
- Debugging a problem is much more difficult. For example, a bug can’t be replicated when a page is within an iFrame but is loaded without an issue when outside the iFrame
- Communication across iFrames requires a special channel such as window.postMessage()
- Each time content in the iFrame needs to change, it will trigger a complete reload
- General issues with the scrollbar for the overflow layout


#### Single SPA

Single-spa is a JavaScript framework for bringing together multiple micro frontends in a single front-end application. Single-spa has been a go-to framework for micro frontend integration for our teams, and they're finding it to work well with SystemJS and managing different versions of a single dependency.

![image](https://user-images.githubusercontent.com/12683240/214583926-10293d3b-76aa-4cf8-a650-810d085c1ae5.png)

Pros
- The main benefit was improving the developer experience. Each Single-SPA app is developed separately, so when a developer starts to work on a React app (Single-SPA app) he/she does not need to install all the dependencies for other apps, like Angular, or to know how other apps are configured. Also because each app is small the development cycle of local builds, hot-reloads, and tests are much shorter in time. Developers can build features (Single-SPA apps) truly independently and separately. So now we could use all the experiences of our React developers in our legacy website.

- Each app in single-SPA is bundled separately. Using different apps for different features results in multiple small chunks, instead of a big fat bundle. Splitting the bundle can also be done by configuring Webpack without Single-SPA, but here we got it for free.

- Apart from smaller chunks and bundles we got lazy loading too. Some features are not used frequently, so their bundle can be loaded separately in the background after the initial load.

- As new feature apps are developed using React, even after migration to a whole new framework like NextJS in the future, those parts can be re-used without the need to rewrite everything from scratch.

Cons
- One issue I had was that I could not generate source maps for Angular when it was built as a SystemJS module. I did not dig deep into the issue as it did not have a great impact on the project. But it is was nice to have source maps.

- Another issue was the integration between the apps. We used local storage, global events, and shared modules for this and they all worked pretty well. But deciding on the best option was sometimes challenging.

- Also as the whole concept is new, it took some time for the new developers to learn how to get on track, although this was negligible and even sometimes exciting to learn about new trends.

#### Module Federation

Module Federation allows JavaScript applications to dynamically import code from another application at run-time. It mainly tackles the problem of code dependency and increased bundle size by enabling dependency sharing.  

Module Federation is a more efficient approach to sharing code and exposing any code from any application. The same code can be used in different environments, such as web, Node.js, and so on.  

The Module Federation is actually part of Webpack config. This config enables us to expose or receive different parts of the CRA to another CRA project. These separate project should not have dependencies between each other, so they can be developed and deployed individually.

![image](https://user-images.githubusercontent.com/12683240/214583962-ff6b1033-bd52-49f2-8706-657d63b1e75f.png)

Pros
- Easier to maintain
- Easier to test
- Independent deploy
- Increases scalability of the teams

Cons
- Requires lots of configuration
- If one of the projects crashes may affect other micro-frontends as well
- Having multiple projects run on the background for the development

When used

- You have a complex project that is expanding fast but without structure.
- You can split your project into multiple self-sufficient parts
- The project can be developed between different teams.
- You are using a frontend framework (Angular, Vue, React) for the long term.

When not used

- Your application is a small business process
- You are not sure and stable with your framework and major versions
- One of the micro frontends want to switch to a different framework
- You do not use Webpack 5 as a module bundler
- Your application is on an old Angular version < 11.0.0

![image](https://user-images.githubusercontent.com/12683240/214584069-ddb45ad3-8ace-405b-9301-9c2b77606c6a.png)


## Approaches using Module Federation

Multiple separate builds should form a single application. These separate builds should not have dependencies between each other, so they can be developed and deployed individually.

Keywords:
- Shell: is a top-level application, which is responsible for consuming and organizing other remote applications or components.

- Remote: is a remote application or component, which is exposed and can be consumed by other components. It must have a unique identifier, so that the shell can distinguish between several of these.

### Approach 1:  Consume react app and angular app from master app.

1. Description 

In this approach, you have a master project, which can be done in react or angular, and this will be responsible for consuming and orchestrating the child applications.

![image](https://user-images.githubusercontent.com/12683240/214584107-4226361c-9eee-43d9-8347-8ad3c4b1d2a7.png)

2. Advantages 

- Great independence to organize the components by the shell/master.

3. Disadvantages

- You need to create a new project as shell/master. And this will also require a repository and its corresponding CI/CD.
- Possible collision in global styles
- Note: a monorepo can also be used. however, a bottleneck could be generated in the code integrations, since several teams would be generating changes on the same repository.

### Approach 2:  Consume all react application in Angular
1. Description 

The shell/master application, in addition to orchestrating external components. It will also have business logic. In this case, the shell will consume an entire remote application, so repetitive components such as login, navigation bar, should be removed or hidden somewhere.

![image](https://user-images.githubusercontent.com/12683240/214584154-8216fa33-8296-4aed-9ba2-8e0ec79b7529.png)

2. Advantages 

- Fewer repositories to maintain.
- Just need to rearrange some views in the shell, to include the remote application

3. Disadvantages

- The remote application will be very dependent on the master, because it will not be able to work independently (the login flow is required to get the tokens and be able to make requests to the database), so when the developers are testing changes, they will necessarily need to raise all environments.
- Possible collision in global styles

### Approach 3:  Consume some modules from react in angular or viceversa

1. Description 

In this approach, what is exposed are components, and not the complete application, as in the previous approaches. This allows you to have your own components and exposed components in both applications, which facilitates organization and independence.

![image](https://user-images.githubusercontent.com/12683240/214584200-923ca77d-33b3-4d02-811b-ced1fb05dbf7.png)

2. Advantages 

Independence in both projects, it will be possible to develop new features without depending on the other application.
Ease of layout, since only specific parts will be exposed.

3. Disadvantages

- Possible problems with exporting global styles from remote components, if they are necessary: for example, components that are difficult to customize that require the use of important!, it will be necessary to make arrangements in the shell to include those styles.


## Experiments

A. Microfront sharing applications

![image](https://user-images.githubusercontent.com/12683240/214584256-728b17d1-bda8-429e-bfad-67a2a267da50.png)

Apply to following approaches:

1. Approach 1: Consume react app and angular app from master app.
2. Approach 2: Consume all react application in Angular


B. Microfront sharing components

![image](https://user-images.githubusercontent.com/12683240/214584293-ed2e804c-096e-4bf2-85c4-cb75393af510.png)

![image](https://user-images.githubusercontent.com/12683240/214584322-e678edea-7fa5-4d02-a329-b74ea147d1cb.png)

Apply to following approaches

1. Approach 3: Consume some modules from react in angular or vice versa


C. Microfront with web Meetpoint application

![image](https://user-images.githubusercontent.com/12683240/214584357-95cb8270-507c-455b-b402-4c96b0f7549e.png)

This project it's only to find quickly posibles problems when we try to implement micro-front in Meetpoint

### Method of communication

Communication can be done using javascript custom events

1. Angular to ReactJS communication

```
  // Publish an event in Angular
  sendMessage(value: string) {
    const event = new CustomEvent('incrementReact', {
      detail: 'sended from Angular...',
    });
    window.dispatchEvent(event);
  }
```

```
  // Listening events from React
  const incrementCount = (event) => {
    setCount((count) => count + 1);
    console.log("I am listening in React this: ", event?.detail);
  };

  useEffect(() => {
    window.addEventListener("incrementReact", incrementCount, true);
    return () => {
      window.removeEventListener("incrementReact", incrementCount, true);
    };
  }, []);
```

2. ReactJS to angular communication

```
   // Publish an event on React
  const receiveMessageHandler = () => {
    const event = new CustomEvent("incrementAngular", {
      detail: "sended from React...",
    });
    window.dispatchEvent(event);
  };
```

```
// Listening events on Angular
  ngOnInit(): void {
    // console.log('When this component has loaded');
    window.addEventListener('incrementAngular', this.incrementValue, true);
  }
  ngOnDestroy(): void {
    window.removeEventListener('incrementAngular', this.incrementValue, true);
  }
  incrementValue = (event: any): void => {
    console.log('I am listening in Angular this: ', event?.detail);
    this.counter++;
  };
```


### Possible errors and how to solve them

1. Possible errors and how to solve them

    1.1. Import meta.error

- You will get the below error while loading angular remote in the host.
- A quick fix for this is to add the below line in remote in webpack.config.js under output property

    ```scriptType : "text/javascript"```

- check here for more detail — https://giters.com/nrwl/nx/issues/7862.

![image](https://user-images.githubusercontent.com/12683240/214584465-313e7272-5a73-4c4f-b7ae-0ad8af387baf.png)


    1.2. Zone.js error

- We get the below error as angular needs zone.js for change detection
- A quick fix to this is to import “zone.js” in the exposed module.

![image](https://user-images.githubusercontent.com/12683240/214584497-5c3e6855-4618-4460-912c-c20214424f3c.png)


    1.3. Public path explicitly error

- A quick fix to this is to set the public path as auto in remote so that webpack automatically determines the path for file chunks, assets(i.e. images, fonts, etc), etc.

```
//e.g. in craco.config.js 
webpackConfig.output.publicPath = “auto”;
```

- Check here for more details — https://webpack.js.org/guides/public-path/#automatic-publicpath

![image](https://user-images.githubusercontent.com/12683240/214584541-946decf8-34d5-4e9d-91cd-9eb16c5dd2bc.png)


    1.4. Eager consumption error

- A quick fix is to load the remote eagerly before the host application starts rendering and for that we need to perform something called chunk loading in host application wherein
- create a file bootstrap.js copy everything from index.js to bootstrap.js
- In index.js just write import (“bootstrap.js”) .

![image](https://user-images.githubusercontent.com/12683240/214584609-463922d9-be51-4494-bf43-5a161b1fb9b9.png)


    1.5. Images not found error

- A quick fix it's convert the images to base64

![image](https://user-images.githubusercontent.com/12683240/214584643-3c6897c8-93a2-4a31-a07f-48120131b61f.png)

    1.6. Conflict with sub dependencies

- A quick fix it's 'npm i --force'


## Implementation effort

1. Approach 1: Consume react app and angular app from master app.

- Create new master project
- Configure angular app for sharing
- Configure react app to share
- Rearrange angular app
- Rearrange react app
- Configure global authentication
- Fix styles
- Implement the communication bus
- Modify the deployment

2. Approach 2: Consume all react application in Angular

- Configure angular app to consume
- Configure react app to share
- Rearrange angular app
- Rearrange react app
- Configure global authentication
- Fix styles
- Implement the communication bus


3. Approach 3: Consume some modules from react in angular or vice versa

- Configure angular app to consume
- Configure react app to share
- Implement react component to share
- Implement angular component to consume
- Fix styles
- Implement the communication bus

## Conclusion

After the analysis, approach 2 was chosen, since only the maps (React) will be exposed, which will be consumed by the Web Application (Angular). And in this way we will avoid having duplicate components (login, navigation bar, etc)

Considerations:
Since the React app will only display maps. When you want to access the route just this. The token will be validated, if it is not available, a message should be displayed "You must access through the Meetpoint Application" or simply redirect to the "MeetPoint Application" page.

## References
- [The History of Microfrontends](https://levelup.gitconnected.com/the-history-of-microfrontends-a8e9e5e9a1d4)
- [Microfrontend a complete guide](https://www.peoplehum.com/blog/micro-frontends-a-complete-guide)
- [Micro frontend guide technical integrations](https://www.trendmicro.com/ru_ru/devops/21/h/micro-frontend-guide-technical-integrations.html)
- [Micro frontend using web components](https://medium.com/swlh/micro-frontend-using-web-components-e9faacfc101b)
- [Micro frontends with module federation](https://ogzhanolguncu.com/blog/micro-frontends-with-module-federation)
- [Micro frontends after one year with single SPA](https://dev.to/psamim/micro-frontends-after-one-year-with-single-spa-1eoo)
- [Micro frontends with angular and modules federation webpack](https://blog.codecentric.nl/rogerdejager/microfrontends-with-angular-and-module-federation-webpack-692)




