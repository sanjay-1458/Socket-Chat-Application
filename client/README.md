# Overview

To create a chap application using socket.io

## Client

The client contains 3 pages: HomePage, LoginPage, and ProfilePage. For routing on this pages

### Routing

Wrap the entire application using `BrowserRouter`. It is used for client side routing in React application using HTML5 history API. It enable us to navigate to different pages without refreshing the pages and `keep UI sync with URL`.
Basically it watches the URL `/home` and matches the current path using `<Route path='/home' element={<HomePage/>/>` and renders the element, and uses the history stack to go forward or backawrd without reloading.
`<Route>` is used to math path/URL with the component. `<Routes>` is the container to all of the `<Route>` elements, first matching route will be rendered. `<Link>` is used to navigate to URL withou reloading pages.

```
<BrowserRouter>
    <App />
  </BrowserRouter>
```
```
<Routes>
    <Route path="/home" element={<HomePage />} />
    <Route path="/login" element={<LoginPage />} />
    <Route path="/profile" element={<ProfilePage />} />
</Routes>
```

### Home Page

The home page is divided into 2 parts for new user and when user clicks on the chat with other participants than the home page is divided into 3 parts; first for showing users where user can be searched with there online presence, the middle part conatins the chat with the user, and the right sideba conatins profile of the user, and media sent.

Here `state lifting` can be seen as the user selcted on left side bar component is also shared in other side bar, therefore a communication is present between the siblings.

```
<Sidebar
    selectedUser={selectedUser}
    setSelectedUser={setSelectedUser}
/>
<ChatContainer
    selectedUser={selectedUser}
    setSelectedUser={setSelectedUser}
/>
<RightSidebar
    selectedUser={selectedUser}
    setSelectedUser={setSelectedUser}
/>
```

We each component recieve the shared state as props.
The right side bar conatins logo, logout, edit profile options and when user click on `Edit Profile`, they are navigated to `Profile Page` here navigation is used via `useNavigation` hook. This is used for navigation because here we want navigation based on logic. Create a search bar for searching users and if it is empty then display each user.

Right sidebar if focused on displaying users, showning whch user is online/offline along with number of unread messages