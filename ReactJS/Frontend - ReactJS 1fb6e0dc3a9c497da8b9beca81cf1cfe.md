# Frontend - ReactJS

## Core concepts

- Components: Ứng dụng React được cấu tạo từ các components, mỗi component là một phần của giao diện người dùng - có riêng logic và giao diện khác nhau. Component có thể là một nút bấm hoặc cũng có thể là cả một trang web
    
    ```jsx
    # tao mot nut bam
    function MyButton() {
      return (
        <button>I'm a button</button>
      );
    }
    
    # co the goi nut bam o component root App
    export default function MyApp() {
      return (
        <div>
          <h1>Welcome to my app</h1>
          <MyButton />
        </div>
      );
    }
    ```
    
    - JSX - Javascript XML: những cú pháp như <h1> được gọi là JSX, JSX được sử dụng trong tất cả các dự án ReactJS
        
        Cú pháp giống HTML nhưng trong React nó là viết gọn của một câu lệnh React để tạo các components
        
        ```jsx
        <h1> Hello World </h1>
        
        import { jsx as _jsx } from "react/jsx-runtime";
        /*#__PURE__*/_jsx("h1", {
          children: " Hello World "
        });
        ```
        
        JSX chặt chẽ hơn HTML. Khi dùng HTML, bạn phải đóng các thẻ như <br />, thành phần của bạn cũng không thể trả về nhiều thẻ JSX.
        
        ```jsx
        function AboutPage() {
          return (
            <>
              <h1>About</h1>
              <p>Hello there.<br />How do you do?</p>
            </>
          );
        }
        ```
        
    - Sử dụng CSS: trong React, bạn chỉ định một lớp CSS với className, nó giống như thuộc tính trong HTML
        
        ```jsx
        <img className="avatar" />
        
        // file CSS
        /* In your CSS */
        .avatar {
          border-radius: 50%;
        }
        ```
        
- Hiển thị dữ liệu: có thể đưa dữ liệu ra bằng cách sử dụng dấu ngoặc nhọn
    
    ```jsx
    return (
      <h1>
        {user.name}
      </h1>
    );
    ```
    
    Cũng có thể sử dụng thêm CSS kết hợp với dữ liệu để cải thiện UI
    
    ```jsx
    const user = {
      name: 'Hedy Lamarr',
      imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
      imageSize: 90,
    };
    
    export default function Profile() {
      return (
        <>
          <h1>{user.name}</h1>
          <img
            className="avatar"
            src={user.imageUrl}
            alt={'Photo of ' + user.name}
            style={{
              width: user.imageSize,
              height: user.imageSize
            }}
          />
        </>
      );
    }
    
    ```
    
- Hiển thị có điều kiện: giống câu lệnh if else
    
    ```jsx
    let content;
    if (isLoggedIn) { content = <AdminPanel />; } 
    else {
      content = <LoginForm />;
    }
    return (<div>{content}</div>);
    
    // don gian hoa code
    <div>
      {isLoggedIn ? (<AdminPanel />) : (<LoginForm />)}
    </div>
    
    //cach 2
    { isLoggedIn && content = <AdminPanel /> }
    ```
    
- Hiển thị danh sách: để hiển thị danh sách component, sử dụng hàm loop hoặc map()
    
    ```jsx
    const people = [
      'Creola Katherine Johnson: mathematician',
      'Mario José Molina-Pasquel Henríquez: chemist',
      'Mohammad Abdus Salam: physicist',
      'Percy Lavon Julian: chemist',
      'Subrahmanyan Chandrasekhar: astrophysicist'
    ];
    
    export default function List() {
      const listItems = people.map(person =>
        <li>{person}</li>
      );
      return <ul>{listItems}</ul>;
    }
    ```
    
- Phản hồi khi có event
    
    Sử dụng thêm option onClick để thêm phản hồi khi có event:
    
    ```jsx
    function MyButton() {
      function handleClick() {
        alert('You clicked me!');
      }
    
      return (
        <button onClick={handleClick}>
          Click me
        </button>
      );
    }
    ```
    
    Hoặc cũng có thể là event bấm nút submit
    
    ```jsx
    function Form() {
      function handleSubmit(e) {
        e.preventDefault();
        console.log('You clicked submit.');
      }
    
      return (
        <form onSubmit={handleSubmit}>
          <button type="submit">Submit</button>
        </form>
      );
    }
    ```
    
- Fragment
    
    Fragment được sử dụng để nhóm một danh sách các Children mà không thêm các thẻ phụ vào DOM. Điều này hữu ích khi bạn muốn trả về nhiều phần tử từ một component mà không muốn tạo thêm các phần tử không cần thiết như **`<div>`** hoặc **`<span>`** bao bọc xung quanh.
    
    ```jsx
    import Fragment
    
    // su dung fragment
    <Fragment> </Fragment>
    
    //cach ngan gon
    <> </>
    ```
    
- Virtual DOM
    
    Thay vì sử dụng DOM như JavasScript thì ReactJS dùng DOM ảo. Virtual DOM là một bản sao của DOM thật dùng để theo dõi các thay đổi trong giao diện người dùng.
    
    Khi có thay đổi, các thay đổi được cập nhập trên virtual DOM và so sánh nó với DOM thật, sau đó React chỉ thay đổi những node cần thiết để tiết kiệm tài nguyên
    
- State
    
    Component thường thay đổi trạng thái hiển thị sau khi tương tác với user. Component cần ghi nhớ những dữ liệu từ user như: giá trị nhập vào, những đồ đã cho vào giỏ hàng… Những dữ liệu cần ghi nhớ như vậy gọi là state
    
    ```jsx
    import { useState } from 'react';
    import { sculptureList } from './data.js';
    
    export default function Gallery() {
      const [index, setIndex] = useState(0);
    
      function handleClick() {
        setIndex(index + 1);
      }
    
      let sculpture = sculptureList[index];
      return (
        <>
          <button onClick={handleClick}>
            Next
          </button>
          <h3>  
            ({index + 1} of {sculptureList.length})
          </h3>
          <img 
            src={sculpture.url} 
            alt={sculpture.alt}
          />
        </>
      );
    }
    
    ```
    
- Lifecycle methods (bổ sung) - đi sâu
    
    Trong ứng dụng với nhiều component, việc giải phóng tài nguyên của component rất quan trọng khi component bị huỷ
    
    Lifecycle methods là những method sử dụng để xử lý các sự kiện xảy ra trong vòng đời của một component. Ví dụ mỗi khi class component được render trong DOM, ta sẽ sử dụng những method “mount” và khi component bị xoá khỏi DOM, sử dụng method “unmount”
    
    Lifecycle chỉ có sẵn trong các class component
    
    ```jsx
    class Clock extends React.Component {
      constructor(props) {
        super(props);
        this.state = {date: new Date()};
      }
    
      componentDidMount() {
        this.timerID = setInterval(
          () => this.tick(),
          1000
        );
      }
    
      componentWillUnmount() {
        clearInterval(this.timerID);
      }
    
      tick() {
        this.setState({
          date: new Date()
        });
      }
    
      render() {
        return (
          <div>
            <h1>Hello, world!</h1>
            <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
          </div>
        );
      }
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<Clock />);
    ```
    
    Tuy nhiên, với sự ra đời của hook function ta có thể thực hiện những yêu cầu tương tự một cách dễ dàng và linh hoạt.
    
    Có 3 giai đoạn chính trong vòng đời 1 component:
    
    - Mouting: gồm các methods:
        - constructor
            
            phương thức khởi tạo trước khi component được mount
            
            sử dụng để khởi tạo state và bind các phương thức trong class
            
        - static getDerivedStateFromProps(prop, state)
            
            phương thức gọi trước khi render, cho phép cập nhập state dựa trên props ban đầu
            
        - render
            
            phương thức bắt buộc trong class
            
            trả về các phần tử Rect được hiển thị trong DOM
            
        - componentDidMount
            
            gọi ngay sau khi mount, thực hiện các thao tác gây tác động như fetch dữ liệu từ server
            
    - Updating
        - static getDerivedStateFromProps: gọi mỗi khi nhận props mới và cho phép cập nhật state
        - shouldComponentUpdate: cho phép quyết định liệu component có nên re-render hay ko (mặc định là true)
        - render: chạy mỗi khi có sự thay đổi trong props hoặc state
        - getSnapShotBeforeUpdate: Phương thức này được gọi ngay trước khi output DOM của component được render lại. Nó có thể trả về một giá trị sẽ được truyền vào componentDidUpdate.
        - **componentDidUpdate(prevProps, prevState, snapshot)**: Phương thức này được gọi ngay sau khi việc cập nhật render hoàn tất. Nó là nơi tốt để thao tác với DOM hoặc thực hiện các thao tác khác sau khi component đã được cập nhật.
    - Unmounting
        
        componentWillUnmount: Phương thức này được gọi ngay trước khi component bị gỡ bỏ khỏi DOM. Đây là nơi để thực hiện các thao tác dọn dẹp như hủy bỏ các timer, hủy bỏ các đăng ký sự kiện, hoặc hủy bỏ các yêu cầu network.
        
- Truyền dữ liệu vào component bằng props
    
    Properties (hay props) cho phép truyền dữ liệu từ component cha xuống những component con, có thể truyền dữ liệu hoặc cả function
    
    ```jsx
    import React from 'react';
    
    interface GreetingProps {
      name: string;
      age?: number;
    }
    
    const Greeting(GreetingProps: props) {
      return (
        <div>
          <h1>Hello, {props.name}!</h1>
          {props.age && <p>You are {props.age} years old.</p>}
        </div>
      );
    };
    
    export default Greeting;
    
    ```
    
    Children props là một props đặc biệt giúp truyền các phần tử con vào component. Children có thể truyền component vào component
    
    ```jsx
    import React from 'react';
    
    interface CardProps {
      title: string;
      children: React.ReactNode;
    }
    
    const Card: React.FC<CardProps> = ({ title, children }) => {
      return (
        <div className="card">
          <h2>{title}</h2>
          <div className="card-content">{children}</div>
        </div>
      );
    };
    
    export default Card;
    
    // component cha
    const App: React.FC = () => {
      return (
        <div>
          <Card title="Card 1">
            <p>This is the content of card 1.</p>
          </Card>
          <Card title="Card 2">
            <p>This is the content of card 2.</p>
            <button>Click me</button>
          </Card>
        </div>
      );
    };
    
    export default App;
    ```
    
- So sánh Props và State
    
    
    | Props | State |
    | --- | --- |
    | Là dữ liệu đầu vào được đưa vào components để hoạt động | Là dữ liệu bên trong components và có thể bị thay đổi khi components hoặt động |
    | Là dữ liệu read-only | Là dữ liệu thường xuyên thay đổi  |
    | Khi props thay đổi, DOM cũng thay đổi và render trang mới | Khi state thay đổi, DOM thay đổi và render trang mới |
- Chia sẻ state giữa 2 components
    
    Lift state lên cho component cha của 2 component đó
    
    ```jsx
    import { useState } from 'react';
    
    export default function Accordion() {
    // day state len component cha
      const [activeIndex, setActiveIndex] = useState(0);
      return (
        <>
          <h2>Almaty, Kazakhstan</h2>
          <Panel
            title="About"
            isActive={activeIndex === 0}
            onShow={() => setActiveIndex(0)}
          >
            With a population of about 2 million, Almaty is Kazakhstan's largest city. From 1929 to 1997, it was its capital city.
          </Panel>
          <Panel
            title="Etymology"
            isActive={activeIndex === 1}
            onShow={() => setActiveIndex(1)}
          >
            The name comes from <span lang="kk-KZ">алма</span>, the Kazakh word for "apple" and is often translated as "full of apples". In fact, the region surrounding Almaty is thought to be the ancestral home of the apple, and the wild <i lang="la">Malus sieversii</i> is considered a likely candidate for the ancestor of the modern domestic apple.
          </Panel>
        </>
      );
    }
    
    function Panel({title, children, isActive, onShow}) 
    {
      return (
        <section className="panel">
          <h3>{title}</h3>
          {isActive ? (
            <p>{children}</p>
          ) : (
            <button onClick={onShow}>
              Show
            </button>
          )}
        </section>
      );
    }
    
    ```
    
- Thinking in React
    
    ![react (1).png](Frontend%20-%20ReactJS%201fb6e0dc3a9c497da8b9beca81cf1cfe/react_(1).png)
    
    Để thiết kế table như này, ta break ra thành 5 component 
    
    ![react (2).png](Frontend%20-%20ReactJS%201fb6e0dc3a9c497da8b9beca81cf1cfe/react_(2).png)
    
    Sau đó thiết kế:
    
    ```jsx
    FilterableProductTable
    	SearchBar
    	ProductTable
    		ProductCategoryRow
    		ProductRow
    ```
    
- Router
    
    React ko hỗ trợ router nên cần cài thư viện là react-router
    
    Router cho phép bạn định tuyến luồng dữ liệu (data flow) trong ứng dụng của bạn một cách rõ ràng
    
    Nếu bạn có URL này, nó sẽ tương đương với router này và giao diện tương ứng
    
    ![Untitled](Frontend%20-%20ReactJS%201fb6e0dc3a9c497da8b9beca81cf1cfe/Untitled.png)
    
    Các thành phần trong React Router:
    
    - Router
        
        Là thành phần bao bọc toàn bộ ứng dụng, cung cấp ngữ cảnh cho các thành phần con để chúng có thể truy cập vào các chức năng của router
        
        **BrowserRouter**: Sử dụng HTML5 history API (pushState, replaceState, và popstate sự kiện) để giữ URL đồng bộ với giao diện của bạn.
        
        **HashRouter**: Sử dụng URL hash (phần sau **`#`** trong URL) để giữ giao diện của bạn đồng bộ với URL.
        
        Thường sử dụng BrowserRouter
        
    - Route
        
        Route được sử dụng để định nghĩa các đường dẫn URL mapping với component và xác định thành phần nào sẽ được render khi đường dẫn đó khớp
        
        ```jsx
        <Route path="/about" component={About} />
        
        <Route path="/about" render={() => <About />} />
        
        // vi du thuc te 
        <Router>
            <div className="App">
                <Route path="/" exact component={Home} />
                <Route path="/about" component={About} />
                <Route path="/contact" component={Contact} />
                <Route component={NotFound}/>
            </div>
        </Router>
        
        ```
        
    - Switch
        
        Switch bọc các route và chỉ render cái đầu tiên mà khớp với URL hiện tại. Điều này rất hữu ích để xác định chỉ một route sẽ được render tại một thời điểm
        
        ```jsx
        <Switch>
          <Route path="/about" component={About} />
          <Route path="/users" component={Users} />
          <Route path="/" component={Home} />
        </Switch>
        ```
        
    - Link
        
        Link được sử dụng để tạo các liên kết điều hướng trong ứng dụng 
        
        ```jsx
        <Link to="/about">About</Link>
        
        ```
        
    - NavLink
        
        Tương tự như Link nhưng nó có thêm các class đặc biệt khi đường dẫn khớp, giúp dễ dàng tạo navigation menu với các mục được đánh dấu khi chúng đang hoạt động
        
        ```jsx
        <NavLink to="/about" activeClassName="active">About</NavLink>
        
        ```
        
    - Tham số URL
        
        Sử dụng tham số để tạo đường dẫn động
        
        ```jsx
        <Route path="/users/:id" component={UserDetail} />
        
        // Trong component UserDetail
        function UserDetail({ match }) {
          return <h2>User ID: {match.params.id}</h2>;
        }
        ```
        
    - Truy vấn
        
        ```jsx
        <Route path="/search" component={SearchPage} />
        
        // Trong component SearchPage
        function SearchPage({ location }) {
          const query = new URLSearchParams(location.search);
          const keyword = query.get('keyword');
          return <h2>Search Keyword: {keyword}</h2>;
        }
        ```
        
    - Match
        
        Khi bạn muốn lấy một số thông tin ở trên URL thì bạn có thể dùng đối tượng match để lấy dữ liệu về. 
        
    - Prompt - xác nhận trước khi chuyển trang
        
        ```jsx
        import {Prompt} from 'react-router-dom';
        
        <Prompt 
            when={true} // true | false
            message={ (location) => (`Ban chac chan muon di den ${location.pathname}`) }
        />
        ```
        
    - Redirect - chuyển trang
        
        ```jsx
        {
            path : '/login',
            exact : false,
            main : ({location}) => <Login location={location} />
        }
        
        ```
        
- API request (axios, use-query or fetch)
    - Fetch
        
        **`fetch`** là một API gốc của JavaScript được sử dụng để thực hiện các yêu cầu HTTP. Nó có cú pháp đơn giản và được tích hợp sẵn trong các trình duyệt hiện đại.
        
        ```jsx
        import React, { useEffect, useState } from 'react';
        
        const FetchExample = () => {
          const [data, setData] = useState(null);
          const [loading, setLoading] = useState(true);
          const [error, setError] = useState(null);
        
          useEffect(() => {
            fetch('https://api.example.com/data')
              .then((response) => {
                if (!response.ok) {
                  throw new Error('Network response was not ok');
                }
                return response.json();
              })
              .then((data) => {
                setData(data);
                setLoading(false);
              })
              .catch((error) => {
                setError(error);
                setLoading(false);
              });
          }, []);
        
        ```
        
    - Axios
        
        **`axios`** là một thư viện HTTP client phổ biến, cung cấp cú pháp thân thiện và nhiều tính năng nâng cao hơn so với **`fetch`**.
        
        ```jsx
        import React, { useEffect, useState } from 'react';
        import axios from 'axios';
        
        const AxiosExample = () => {
          const [data, setData] = useState(null);
          const [loading, setLoading] = useState(true);
          const [error, setError] = useState(null);
        
          useEffect(() => {
            axios.get('https://api.example.com/data')
              .then((response) => {
                setData(response.data);
                setLoading(false);
              })
              .catch((error) => {
                setError(error);
                setLoading(false);
              });
          }, []);
        
        ```
        
    - Use-query
        
        **`react-query`** (hiện được đổi tên thành **`@tanstack/react-query`**) là một thư viện mạnh mẽ để quản lý và truy vấn dữ liệu trong các ứng dụng React. Nó giúp quản lý trạng thái của các yêu cầu API một cách hiệu quả và cung cấp nhiều tính năng như caching, re-fetching, và syncing với server state.
        
        ```jsx
        import React from 'react';
        import { useQuery, QueryClient, QueryClientProvider } from '@tanstack/react-query';
        import axios from 'axios';
        
        // Khởi tạo query client
        const queryClient = new QueryClient();
        
        const fetchData = async () => {
          const { data } = await axios.get('https://api.example.com/data');
          return data;
        };
        
        const ReactQueryExample = () => {
          const { data, error, isLoading } = useQuery(['data'], fetchData);
        
          if (isLoading) return <div>Loading...</div>;
          if (error) return <div>Error: {error.message}</div>;
        
          return (
            <div>
              <pre>{JSON.stringify(data, null, 2)}</pre>
            </div>
          );
        };
        
        const App = () => (
          <QueryClientProvider client={queryClient}>
            <ReactQueryExample />
          </QueryClientProvider>
        );
        
        export default App;
        
        ```
        
- Context Provider
    
    Context provider được sử dụng để cung cấp giá trị của một context cho tất cả các component trong cây component mà không cần truyền props qua từng lớp
    
    Điều này rất hữu ích khi cần chia sẻ dữ liệu hoặc các hàm giữa nhiều component mà không muốn truyền props qua nhiều lớp
    
    ```jsx
    // MyContext.js
    import React from 'react';
    
    const MyContext = React.createContext();
    
    export default MyContext;
    
    // MyProvider.js
    import React, { useState } from 'react';
    import MyContext from './MyContext';
    
    const MyProvider = ({ children }) => {
      const [state, setState] = useState({ someValue: 'initialValue' });
    
      return (
        <MyContext.Provider value={{ state, setState }}>
          {children}
        </MyContext.Provider>
      );
    };
    
    export default MyProvider;
    
    // App.js
    import React from 'react';
    import MyProvider from './MyProvider';
    import MyComponent from './MyComponent';
    
    const App = () => (
      <MyProvider>
        <MyComponent />
      </MyProvider>
    );
    
    export default App;
    
    // MyComponent.js
    import React, { useContext } from 'react';
    import MyContext from './MyContext';
    
    const MyComponent = () => {
      const { state, setState } = useContext(MyContext);
    
      return (
        <div>
          <p>{state.someValue}</p>
          <button onClick={() => setState({ someValue: 'newValue' })}>Update</button>
        </div>
      );
    };
    
    export default MyComponent;
    
    ```
    
- State management
    
    Quản lý state (state management) trong React là một phần quan trọng để xây dựng các ứng dụng web phức tạp. State quản lý dữ liệu động và tình trạng của một component, và việc quản lý state đúng cách giúp đảm bảo ứng dụng của bạn hoạt động trơn tru và dễ bảo trì. Có nhiều cách để quản lý state trong React, từ các cách đơn giản như sử dụng state cục bộ trong component cho đến các thư viện quản lý state phức tạp hơn như Redux hoặc MobX.
    
    Có 2 thư viện phổ biến sử dụng để quản lý state:
    
    - Redux
        
        ![Untitled](Frontend%20-%20ReactJS%201fb6e0dc3a9c497da8b9beca81cf1cfe/Untitled%201.png)
        
        Redux sử dụng một store toàn cục để quản lý state của ứng dụng
        
        ```jsx
        // store.js
        import { createStore } from 'redux';
        
        const initialState = { count: 0 };
        
        function counterReducer(state = initialState, action) {
          switch (action.type) {
            case 'INCREMENT':
              return { count: state.count + 1 };
            case 'DECREMENT':
              return { count: state.count - 1 };
            default:
              return state;
          }
        }
        
        const store = createStore(counterReducer);
        
        export default store;
        
        // App.js
        import React from 'react';
        import { Provider, useSelector, useDispatch } from 'react-redux';
        import store from './store';
        
        const Counter = () => {
          const count = useSelector(state => state.count);
          const dispatch = useDispatch();
        
          return (
            <div>
              <p>Count: {count}</p>
              <button onClick={() => dispatch({ type: 'INCREMENT' })}>Increment</button>
              <button onClick={() => dispatch({ type: 'DECREMENT' })}>Decrement</button>
            </div>
          );
        };
        
        const App = () => (
          <Provider store={store}>
            <Counter />
          </Provider>
        );
        
        export default App;
        
        ```
        
    - Zustand
        
        Zustand là một thư viện quản lý state đơn giản nhưng mạnh mẽ, không cần boilerplate nhiều như Redux.
        
        ```jsx
        // store.js
        import create from 'zustand';
        
        const useStore = create(set => ({
          count: 0,
          increment: () => set(state => ({ count: state.count + 1 })),
          decrement: () => set(state => ({ count: state.count - 1 }))
        }));
        
        export default useStore;
        
        // App.js
        import React from 'react';
        import useStore from './store';
        
        const Counter = () => {
          const { count, increment, decrement } = useStore();
          return (
            <div>
              <p>Count: {count}</p>
              <button onClick={increment}>Increment</button>
              <button onClick={decrement}>Decrement</button>
            </div>
          );
        };
        
        const App = () => (
          <div>
            <Counter />
          </div>
        );
        
        export default App;
        
        ```
        
    - Recoil - trending
        
        Recoil là một thư viện quản lý state của Facebook, cung cấp một cách tiếp cận mới mẻ cho quản lý state trong React. Recoil dễ dàng kết hợp với hook và cung cấp khả năng quản lý state phức tạp với các phụ thuộc lẫn nhau.
        
        ```jsx
        // atoms.js
        import { atom } from 'recoil';
        
        export const countState = atom({
          key: 'countState',
          default: 0,
        });
        
        // App.js
        import React from 'react';
        import { RecoilRoot, useRecoilState } from 'recoil';
        import { countState } from './atoms';
        
        const Counter = () => {
          const [count, setCount] = useRecoilState(countState);
          return (
            <div>
              <p>Count: {count}</p>
              <button onClick={() => setCount(count + 1)}>Increment</button>
              <button onClick={() => setCount(count - 1)}>Decrement</button>
            </div>
          );
        };
        
        const App = () => (
          <RecoilRoot>
            <Counter />
          </RecoilRoot>
        );
        
        export default App;
        
        ```
        
    - Redux Toolkit - trending
        
        Redux Toolkit đã trở thành tiêu chuẩn de facto để viết Redux logic. Nó giúp giảm thiểu boilerplate, cung cấp cấu trúc rõ ràng và tích hợp các công cụ như Redux Thunk một cách tự nhiên
        
        ```jsx
        // store.js
        import { configureStore, createSlice } from '@reduxjs/toolkit';
        
        const counterSlice = createSlice({
          name: 'counter',
          initialState: { count: 0 },
          reducers: {
            increment: state => { state.count += 1; },
            decrement: state => { state.count -= 1; }
          }
        });
        
        export const { increment, decrement } = counterSlice.actions;
        export default configureStore({ reducer: counterSlice.reducer });
        
        // App.js
        import React from 'react';
        import { Provider, useSelector, useDispatch } from 'react-redux';
        import store, { increment, decrement } from './store';
        
        const Counter = () => {
          const count = useSelector(state => state.count);
          const dispatch = useDispatch();
        
          return (
            <div>
              <p>Count: {count}</p>
              <button onClick={() => dispatch(increment())}>Increment</button>
              <button onClick={() => dispatch(decrement())}>Decrement</button>
            </div>
          );
        };
        
        const App = () => (
          <Provider store={store}>
            <Counter />
          </Provider>
        );
        
        export default App;
        
        ```
        
    - Jotai - trending
    - Valtio - trending
    
    Flow hoạt động:
    
    ![Untitled](Frontend%20-%20ReactJS%201fb6e0dc3a9c497da8b9beca81cf1cfe/Untitled%202.png)
    
- So sánh component và element
    - **`component`**: Được sử dụng trong các phiên bản trước của **`react-router-dom`**. Bạn truyền vào một tham chiếu component.
        
        React Router sẽ tự động tạo ra một phần tử từ component đó khi tuyến đường khớp.
        
    - **`element`**: Được sử dụng trong **`react-router-dom`** phiên bản 6 trở lên. Bạn truyền vào một phần tử JSX.
        
        Với **`element`**: Bạn tạo phần tử ngay tại chỗ và truyền nó vào thuộc tính **`element`**.
        

### React Hook

- Khái niệm & Lợi ích
    
    **Quản lý state và life cycle của component dễ dàng hơn**: Trước khi có React Hooks, state và life cycle ****của React components thường chỉ được quản lý trong Class Components. Functional Components không có khả năng quản lý trạng thái hoặc thực hiện các tác vụ sau khi render. React Hooks giúp bạn sử dụng trạng thái và vòng đời trong Functional Components một cách dễ dàng và hiệu quả.
    
- Một số yêu cầu khi sử dụng
    1. Hook State và Effect Queues
        
        React quản lý state và effect của hooks bằng cách sử dụng các queues (hàng đợi). Khi một component sử dụng hook, React sẽ đặt các state và effect vào hàng đợi của component đó
        
        Mỗi component có một danh sách các hooks được gọi theo thứ tự. React sử dụng thứ tự này để theo dõi và cập nhật đúng hook state cho đúng component.
        
    2. Chỉ được gọi trong component function
        
        Hooks phải được gọi trong thân hàm của component hoặc trong các hàm custom hook. Điều này đảm bảo rằng các hooks được gọi theo cùng một thứ tự mỗi khi component được render.
        
    3. Render phases
        
        Trong quá trình render, React sẽ gọi hàm component và đồng thời xử lý các hooks.
        
        Khi component được render lần đầu, React sẽ ghi nhớ thứ tự các hooks và lưu trữ state ban đầu của chúng.
        
        Trong các lần render tiếp theo, React sẽ sử dụng thứ tự này để khôi phục và cập nhật state cho từng hook.
        
- Cơ chế hoạt động
    
    ![Untitled](Frontend%20-%20ReactJS%201fb6e0dc3a9c497da8b9beca81cf1cfe/Untitled%203.png)
    
    ![Untitled](Frontend%20-%20ReactJS%201fb6e0dc3a9c497da8b9beca81cf1cfe/Untitled%204.png)
    
    ![Untitled](Frontend%20-%20ReactJS%201fb6e0dc3a9c497da8b9beca81cf1cfe/Untitled%205.png)
    
    Trong React, cơ chế quản lý state của hook được thực hiện thông qua một hệ thống nội bộ quản lý “queue” cho mỗi component. 
    
    - Fiber và Execution Context:
        
        React sử dụng kiến trúc gọi là fiber để quản lý và lên lịch cho việc cập nhật component, mỗi component được đại diện bởi một fiber
        
        Mỗi lần một component render, React tạo ra một execution context (ngữ cảnh thực thi) mới cho component đó. Execution context này bao gồm các thông tin cần thiết để quản lý và theo dõi state của hook
        
    - Hook state list
        
        mỗi functional component có một danh sách state hook gọi là “hook state list”, danh sách này lưu trữ các giá trị state và các tham chiếu đến các hook khác
        
        khi component render, React sẽ duyệt qua danh sách này theo thứ tự các hook được gọi
        
    - current hook and work in progress book
    React sử dụng hai biến nội bộ là `currentHook` và `workInProgressHook` để theo dõi trạng thái hiện tại và trạng thái đang tiến hành của các hooks trong quá trình render.
    
    Khi một component bắt đầu render, `currentHook` được đặt lại về null và `workInProgressHook` được liên kết với danh sách hook state hiện tại của component đó.
    - Queue cho các update
    Khi state của một hook được cập nhật (ví dụ: gọi `setCount`), React không cập nhật ngay lập tức mà thêm cập nhật này vào một "queue" (hàng đợi) của hook đó.
    
    Mỗi lần render mới, React sẽ xử lý tất cả các cập nhật trong hàng đợi theo thứ tự chúng được thêm vào. Điều này đảm bảo rằng các cập nhật state được thực hiện theo đúng thứ tự và không bỏ lỡ bất kỳ cập nhật nào.
    - commit phase
        
        Sau khi tất cả các hooks được gọi và danh sách hook state được cập nhật, React sẽ tiến hành "commit phase".
        
        Trong phase này, React sẽ thực hiện các thay đổi state thực tế và cập nhật DOM nếu cần thiết.
        
- Cơ chế hoạt động của class component thông thường
    
    Trong các class component của React, quản lý state được thực hiện bằng cách sử dụng thuộc tính `state` và phương thức `setState`
    
- useState
    
    useState giúp thêm các state vào component mà không cần phải tạo class
    
    Nó cung cấp biến state và một hàm để cập nhập state
    
    ```jsx
    import React, { useState } from 'react';
    
    function ExampleComponent() {
      // Khởi tạo trạng thái với giá trị ban đầu là 0
      const [count, setCount] = useState(0);
    
      // Hàm tăng giá trị trạng thái
      const incrementCount = () => {
        setCount(count + 1); // Gọi hàm setCount để cập nhật trạng thái
      }
    
      return (
        <div>
          <p>Count: {count}</p>
          <button onClick={incrementCount}>Increment</button>
        </div>
      );
    }
    ```
    
- useEffect
    
    là hook quan trọng của React, sử dụng để thực hiện các side effect trong các function của component
    
    Các side effect là các tác vụ không ảnh hưởng trực tiếp tới việc hiển thị của component như gọi API, thao tác với DOM hay đăng ký các sự kiện
    
     `useEffect()` cho phép bạn thực hiện các tác vụ tại các điểm quan trọng trong vòng đời của một component React, như sau khi component được tạo (componentDidMount) hoặc sau khi nó được cập nhật (componentDidUpdate). Điều này giúp bạn quản lý tất cả các tác vụ "side effects" một cách dễ dàng.
    
    ‘useEffect’ sử dụng để thực thi các side effect sau mỗi lần component được render hoặc sau khi thay đổi state. Nó chạy sau mỗi lần render
    
    ```jsx
     useEffect(() => {
      // Thực hiện các side effect ở đây
    }, [dependencies]);
    ```
    
    ‘dependencies’ là một mảng chứa các giá trị khiến cho useEffect chạy lại. Nếu dependencies trống, ‘useEffect sẽ chạy sau mỗi lần rerender’ , nếu dependencies ko được cung cấp, ‘useEffect’ chỉ chạy sau lần render đầu tiên
    
    ```jsx
    import React, { useState, useEffect } from 'react';
    
    function Example() {
      const [count, setCount] = useState(0);
    
      // Thực hiện side effect sau mỗi lần render và sau khi `count` thay đổi
      useEffect(() => {
        document.title = `You clicked ${count} times`;
      }, [count]);
    
      return (
        <div>
          <p>You clicked {count} times</p>
          <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
      );
    }
    
    export default Example;
    
    // Trong ví dụ này, document.title sẽ được cập nhật sau mỗi lần count thay đổi,
    // với giá trị mới là số lần click.
    ```
    
    - Clean-up trong ‘useEffect’:
        
        Ngoài việc thực hiện side effect, bạn cũng có thể thực hiện các tác vụ clean-up khi component bị unmount hoặc trước khi side effect mới được thực thi. Để làm điều này, bạn có thể return một hàm từ hàm effect:
        
        ```jsx
        useEffect(() => {
          // Thực hiện side effect ở đây
        
          return () => {
            // Thực hiện các tác vụ clean-up ở đây
          };
        }, [dependencies]);
        ```
        
        Ví dụ:
        
        ```jsx
        import React, { useState, useEffect } from 'react';
        
        function Timer() {
          const [time, setTime] = useState(0);
        
          useEffect(() => {
            const timerId = setInterval(() => {
              setTime(time => time + 1);
            }, 1000);
        
            // Clean-up: Hủy bỏ interval khi component unmount
            return () => {
              clearInterval(timerId);
            };
          }, []); // Dependency trống nên useEffect chỉ chạy một lần sau lần render đầu tiên
        
          return (
            <div>
              <p>Timer: {time}s</p>
            </div>
          );
        }
        
        export default Timer;
        ```
        
- useContext
    
    `useContext` là một hook trong React được sử dụng để truy cập các giá trị của một Context API. Context API trong React là một cách để truyền dữ liệu từ một thành phần cha đến các thành phần con mà không cần truyền props qua nhiều lớp con trung gian `useContext` giúp bạn lấy giá trị từ Context API một cách dễ dàng.
    
    ```jsx
    import React, { createContext } from 'react';
    
    const MyContext = createContext();
    ```
    
- useReducer
    
    `useReducer` là một hooks được sử dụng để quản lý trạng thái (state) và hành động (actions) của ứng dụng. `useReducer` gần giống với `useState`, tuy nhiên nó thường được sử dụng khi bạn cần quản lý một trạng thái phức tạp hơn và khi trạng thái của bạn có quá nhiều hành động gây ra sự thay đổi
    
    ```jsx
    import React, { useReducer } from 'react';
    
    function Counter() {
      const initialState = { count: 0 };
      const [state, dispatch] = useReducer(reducer, initialState);
      
      // Bây giờ 'state' chứa trạng thái hiện tại và 'dispatch' là một hàm để gửi hành động.
      
      // Ví dụ về việc tăng/giảm giá trị count:
      const increment = () => {
        dispatch({ type: 'INCREMENT' });
      };
    
      const decrement = () => {
        dispatch({ type: 'DECREMENT' });
      };
    
      return (
        <div>
          <p>Count: {state.count}</p>
          <button onClick={increment}>Increment</button>
          <button onClick={decrement}>Decrement</button>
        </div>
      );
    }
    ```
    
- useLayoutEffect
    
    `useLayoutEffect` là một hook tương tự `useEffect` trong React, nhưng nó được gọi đồng bộ ngay sau khi các thay đổi trong DOM được áp dụng, trước khi trình duyệt cập nhật giao diện người dùng.
    
    So sánh với useEffect
    
    |  | useEffect | useLayoutEffect |
    | --- | --- | --- |
    | Thời điểm chạy | Chạy bất đồng bộ, sau khi component đã được render và giao diện người dùng đã được cập nhật. Điều này thích hợp cho hầu hết các tác vụ bất đồng bộ. | Chạy đồng bộ, ngay sau khi các thay đổi trong DOM đã được áp dụng và trước khi giao diện người dùng được cập nhật. Điều này đảm bảo rằng tác vụ được thực hiện trước khi người dùng thấy bất kỳ thay đổi gì trong giao diện. Quá trình này có thể làm chậm quá trình render và tạo cảm giác có độ trễ. |
    | Hiệu suất | Thích hợp cho hầu hết các tác vụ bất đồng bộ. useEffect() thường được sử dụng khi bạn cần thực hiện các tác vụ phụ thuộc vào hiệu ứng phụ (side effects) mà không cần phải thực hiện chúng đồng bộ trước khi giao diện người dùng được cập nhật. useEffect không làm chậm quá trình render và làm cho ứng dụng hoạt động nhanh hơn. | Nếu không cẩn thận, useLayoutEffect có thể làm chậm quá trình render và gây ra cảm giác có độ trễ. useLayoutEffect thường được sử dụng cho các tác vụ liên quan đến layout hoặc đồ họa, và khi cần đảm bảo rằng tác vụ được thực hiện ngay lập tức. |
- useMemo
    
    `useMemo` là một trong những hook cung cấp bởi React dùng để tối ưu hóa hiệu suất của ứng dụng bằng cách lưu giữ kết quả của một hàm tính toán và trả về giá trị đó khi các dependencies của nó không thay đổi. Điều này giúp tránh việc tính toán lại giá trị nếu không cần thiết, đặc biệt là trong trường hợp tính toán tốn thời gian.
    
    ```jsx
    const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
    
    //computeExpensiveValue là hàm mà bạn muốn tính toán một giá trị.
    
    //[a, b] là mảng dependencies. Nếu bất kỳ giá trị nào trong mảng này thay đổi, 
    //computeExpensiveValue sẽ được tính toán lại và kết quả mới được trả về.
    ```
    
- ReactMemo
    
    ```jsx
    import React from 'react';
    
    const MyComponent = ({ a, b }) => {
      return <div>{a + b}</div>;
    };
    
    export default React.memo(MyComponent); 
    // MyComponent chỉ render lại nếu a hoặc b thay đổi
    
    // vd2
    import React from 'react';
    
    const MyComponent = ({ a, b }) => {
      return <div>{a + b}</div>;
    };
    
    const areEqual = (prevProps, nextProps) => {
      // Kiểm tra nếu các props không thay đổi
      return prevProps.a === nextProps.a && prevProps.b === nextProps.b;
    };
    
    export default React.memo(MyComponent, areEqual);
    
    ```
    
- Phân biệt useMemo và ReactMemo
    
    
    |  | useMemo | ReactMemo |
    | --- | --- | --- |
    | Mục đích | useMemo là một hook được sử dụng để ghi nhớ giá trị tính toán giữa các lần render. Nó giúp tránh tính toán lại các giá trị không cần thiết nếu các phụ thuộc không thay đổi. | React.memo là một higher-order component (HOC) được sử dụng để ghi nhớ kết quả render của một functional component. Nó giúp tránh render lại component không cần thiết nếu props của nó không thay đổi. |
    | Hoạt động | useMemo nhận vào hai tham số: một hàm tính toán và một mảng phụ thuộc.
    Giá trị trả về của hàm tính toán sẽ được ghi nhớ (memoized) cho đến khi một trong các giá trị trong mảng phụ thuộc thay đổi. | React.memo nhận vào một component và trả về một component mới chỉ render lại nếu props của nó thay đổi.
    Bạn có thể tùy chọn cung cấp một hàm so sánh tùy chỉnh để kiểm tra sự thay đổi của props. |
    | Khi nào nên sử dụng | Khi bạn có các phép tính tốn kém cần được thực hiện chỉ khi các giá trị đầu vào thay đổi.
    Khi bạn muốn tối ưu hóa hiệu suất bằng cách tránh tính toán lại các giá trị không thay đổi. | Khi bạn có một component nhận nhiều props và bạn muốn tránh render lại component đó nếu các props không thay đổi.
    Khi bạn muốn tối ưu hóa hiệu suất cho các component có nhiều props hoặc thực hiện render tốn kém. |
- useCallBack
    
    `useCallback` là một hook trong React được sử dụng để tối ưu hóa hiệu suất của ứng dụng bằng cách lưu giữ một hàm callback và chỉ tính toán lại nó khi các dependencies của nó thay đổi. Điều này đặc biệt hữu ích khi bạn truyền các hàm callback làm props cho các component con, và bạn không muốn component render lại mỗi khi một hàm callback bên ngoài thay đổi.
    
    ```jsx
    const memoizedCallback = useCallback(() => {
      // Hàm callback của bạn ở đây
    }, [dependencies]);
    ```
    
- useRef
    
    `useRef` là một hook trong React được sử dụng để tạo một tham chiếu (reference) đến một phần tử DOM hoặc để lưu trữ các giá trị mà bạn muốn duy trì giữa các chu kỳ render của component mà không gây ra việc render lại khi giá trị thay đổi
    
    ```jsx
    import React, { useRef, useState, useEffect } from 'react';
    
    function ExampleComponent() {
      const countRef = useRef(0);
      const [count, setCount] = useState(0);
    
      const incrementCount = () => {
        // Sử dụng `countRef` để lưu trữ giá trị không gây ra việc render lại
        countRef.current = countRef.current + 1;
    
        // Sử dụng `setCount` để cập nhật giá trị trong state và gây ra việc render lại
        setCount(count + 1);
      };
    
      return (
        <div>
          <p>Count (state): {count}</p>
          <p>Count (ref): {countRef.current}</p>
          <button onClick={incrementCount}>Increment Count</button>
        </div>
      );
    }
    
    export default ExampleComponent;
    ```
    
- useQuery
    
    Là một hook dùng để quản lý việc fetching, caching và updating dữ liệu từ API
    
    Để sử dụng useQuery, cần cài đặt thư viện và bọc component với ‘QueryClientProvider’ để cung cấp ‘Query Client’ cho ứng dụng
    
    ```jsx
    import { QueryClient, QueryClientProvider, useQuery } from '@tanstack/react-query';
    
    const queryClient = new QueryClient();
    
    function App() {
      return (
        <QueryClientProvider client={queryClient}>
          <MyComponent />
        </QueryClientProvider>
      );
    }
    
    function MyComponent() {
      const { isLoading, error, data } = useQuery(['todos'], fetchTodos);
    
      if (isLoading) return <div>Loading...</div>;
      if (error) return <div>Error: {error.message}</div>;
    
      return (
        <div>
          {data.map(todo => (
            <div key={todo.id}>{todo.title}</div>
          ))}
        </div>
      );
    }
    
    async function fetchTodos() {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos');
      return response.json();
    }
    
    ```
    
- Build own hook
    
    Tạo custom hooks trong React cho phép bạn tái sử dụng logic stateful giữa các functional component. Một custom hook chỉ đơn giản là một hàm JavaScript bắt đầu với `use` và có thể gọi các hook khác bên trong nó.
    

### Redux Form

Là một thư viện giúp quản lý trạng thái của các mẫu trong React bằng cách sử dụng redux.

Nó cung cấp một cách tiện lợi để quản lý dữ liệu đầu vào từ các biểu mẫu, xác thực dữ liệu và xử lý các hành động liên quan đến việc gửi dữ liệu từ biểu mẫu 

```jsx
import { createStore, combineReducers } from 'redux';
import { Provider } from 'react-redux';
import { reducer as formReducer } from 'redux-form';

const rootReducer = combineReducers({
  form: formReducer,
  // các reducers khác của bạn
});

const store = createStore(rootReducer);

const App = () => (
  <Provider store={store}>
    <YourMainComponent />
  </Provider>
);

export default App;

//form component file
import React from 'react';
import { Field, reduxForm } from 'redux-form';

// Custom input component
const renderInput = ({ input, label, type, meta: { touched, error } }) => (
  <div>
    <label>{label}</label>
    <div>
      <input {...input} placeholder={label} type={type} />
      {touched && error && <span>{error}</span>}
    </div>
  </div>
);

// Form component
let MyForm = ({ handleSubmit }) => {
  const submit = (values) => {
    console.log(values);
  };

  return (
    <form onSubmit={handleSubmit(submit)}>
      <Field name="username" type="text" component={renderInput} label="Username" />
      <Field name="password" type="password" component={renderInput} label="Password" />
      <button type="submit">Submit</button>
    </form>
  );
};

// Decorate the form component
MyForm = reduxForm({
  form: 'myForm' // a unique identifier for this form
})(MyForm);

export default MyForm;

```

Có thể thêm chức năng validation cho các trường biểu mẫu

```jsx
const required = value => (value ? undefined : 'Required');

let MyForm = ({ handleSubmit }) => {
  const submit = (values) => {
    console.log(values);
  };

  return (
    <form onSubmit={handleSubmit(submit)}>
      <Field name="username" type="text" component={renderInput} label="Username" validate={[required]} />
      <Field name="password" type="password" component={renderInput} label="Password" validate={[required]} />
      <button type="submit">Submit</button>
    </form>
  );
};

MyForm = reduxForm({
  form: 'myForm'
})(MyForm);

export default MyForm;

```

Redux Form lifecycle:

- Initialize form data - khởi tạo giá trị mặc định cho biểu mẫu
- Field-level validation - xác thực các trường cụ thể trong biểu mẫu
- Form-level validation - xác thực toàn bộ biểu mẫu
- Handling submission - quản lý việc submit biểu mẫu và xử lý lỗi submit

Thiếu:

useMemo, ReactMemo → phân biệt

useContext, contexxt, useCallBack

cơ chế đằng sau React Hook

state management - trending

useQuery

react hook quản lý state, logic như nào so với class component

build own hook

xem lại JS6

MUI

twitter -product hunt