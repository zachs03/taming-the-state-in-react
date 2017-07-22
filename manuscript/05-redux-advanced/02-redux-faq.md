# (React in) Redux FAQ

I intend to grow this section organically to answer frequently asked questions to the best of my knowledge. These are questions that come up often when discussing Redux standalong or as complementing to React.

## Redux vs. Local State

When introducing Redux to a React application, people are unsure how to treat the local state with `this.state` and `this.setState()`. Should they replace the local state entirely with Redux or keep a mix of both? The larger part of the community would argue it is the latter and I agree with it. Local state doesn't become obsolete when using a sophisticated state management library like Redux. You can still use it.

Imagine your application grows in line of code and your size of developers working on this application grows as well. Your global state in Redux will necessarly grow too. However, you want to keep the global state meaningful and reusable from multiple parties (developers, components) in your application. That's why not everything should end up in the global state. In a growing application, you should always revisit your global state and make sure that it is not cluttered and arranged thoughtfully.

The cluttering happens when too much state ends up in the global state that is only used by a single party (one component, one component tree). You should think twice about this kind of state and evaluate whether it would make more sense to put in the local state of the (root) component. Always ask yourself: who is interested in this state? A balanced mixture of local state and sophisticated state will make your application maintainable and predictable in the long run.

The boundaries between local state and sophisticated state will blur when using a state management library like MobX. You will get to know this library later as alternative to Redux. But there as well, you can plan your state in your application thoughtfully.

In general, the usage of Redux state should be kept to a minimum. A good rule of thumb is to keep the state close to your component with local state but evaluate later whether another party is interested in the state. If another party has the same state, but only an independent copy of it, you could use a reusable higher order component that manages the state. If the state is shared, you could try to lift your state up or down. However, if lifting state doesn't solve the problem for you, because the state is shared across the application, you should consider to use Redux for it. All of this goes back that you might not need Redux in your application, because local state is sufficient.

- TODO https://www.reddit.com/r/reactjs/comments/6g2kp1/react_state_vs_redux_state_when_and_why/?st=1Z141Z3&sh=255adc41

## View vs. Entity State

In the beginning of the book, I differentiated between view state and entity state. Imagine you have a page that does both displaying a list of items and showing opt-in modals for each item to remove or edit the item. While the former would be the entity state, the latter would be the view state. The entitiy state, the list of items, comes most often from a backend. The view state is triggered by the user only in the frontend. Is there a pattern of where to store which kind of state?

The entity state comes often from the backend. It is fetched asynchronously. In applications, you want to avoid to fetch entities more than once. A good practice would be to fetch the entities once and not again when they are already there. Thus they would have to be stored somewhere where several parties know that these entities are already fetched. The global state is a perfect place to store them.

The view state is altered only in the frontend. Often it isn't shared across the application, because, for instance, only the modal knows if it is opened or closed. Since it doesn't need to be shared, you can use the local state and avoid to clutter in the global state.

Imagine you have a component that has tabs. Each tab has a different perspective on the displayed items. For instance, the user cna choose a grid or a list layout. It is absolutely fine to store this state in the local state. In addition, you can give your user an improved user experience. You could store the selected tab in the local storage of your browser too and when the user returns to the page, you rehydrate the state from the local storage into your local state. The user will always find his/her preffered tab as the selected one.

## Planning State

Can you plan your state? I would argue that you can plan it. You can plan which part of the state goes into the global state and which part goes into the local state. For instance, you know about the view and entitiy states. In addtion, you can put some of your state in the local storage to imporve the user experience. However, in an evolving application your state grows and the structure changes. What can you do about it? My recommendation is always revisiting your state arrangement and structure. There is always room for improvements. You should refactor it early to keep it maintainable and predictable in the long run.