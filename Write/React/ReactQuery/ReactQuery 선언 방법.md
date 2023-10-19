### TypeScript, Vite 프로젝트를 생성해준 후에, ReactQuery 예제를 생성해준다.

1. package.json

```javascript
"@tanstack/react-query": "^4.33.0",
"@tanstack/react-query-devtools": "^4.33.0",
```

2. src/Provider/index.tsx 파일 생성 후, 쿼리 클라이언트 생성
```javascript
const ReactQueryProvider = ({children}: {children: ReactNode}) => {
	//쿼리클라이언트 선언
	const queryClient = new QueryClient({
    	defulatOptions: {
        	queries:  {
            	refetchOnWindowFocus: false,
                staleTime: 5* 60* 1000,
            },
        }
    })
	
    return (
    	<QueryClientProvider client = {queryClient}>{children}</QueryClientProvider>
    )
}

```


3. src/main.tsx 에서 컴포넌트 import

```javascript
ReactDom.createRoot(document.getElementById('root')!).render(
	<React.StrictMode>
    	//2번에서 선언
    	<ReactQueryProvider>
        	<App/>
            <ReactQueryDevtools initialIsOpen={false}/>
		</ReactQueryProvider>
    </React.StrictMode>,
)
```


### React.StrictMode란?

StrictMode는 애플리케이션 내의 잠재적인 문제를 알아내기 위한 도구. UI를 렌더링하지 않으며, 자식노드에 대한 부가적임 검사, 경고문을 띄워줌.


#### baseUrl

axios로, postUrl을 선언해줌.

```javascript
import axios from "axios";

const postUrl = axios.create({
	//예시 URL
    baseURL: "http://localhost:8000/api/post"
})

export default postUrl
```

#### Post interface

types 폴더 내에, Post객체 생성
```javascript
export interface Post {
	title: string;
    content: string;
    category: string;
    //etc
}
```


#### usePostList

```javascript
import postUrl from "./baseUrl.ts"
import {useQuery} from "@tanstack/react-qeury"
import {Post} from "../types/Post.ts"

//postUrl에서 데이터를 비동기로 가져옴
const getPostList = async() => {
	const {data} = await postUrl.get("/")
    return data.data
}

const useGetPostList = () =>
	useQuery<Array<Post>, Error>({
    	//useQuery에 부여되는 고유의 키, queryKey
    	queryKey : ["posts"],
        //Promise 처리가 아뤄지는 함수
        queryFn : () => getPostList()
    })
```

서버의 데이터는, fetching이 반복되어서는 안되고, 

생성/수정/삭제시에 useMutation hook을 사용해야만한다.

```javascript
import postUrl from "./baseUrl.ts";
import {useMutation, useQueryClient} from "@tanstack/react-query";
import {Post} from "../types/Post.ts";

//post
const postPostCreate = async (post:Post) => {
    const {data} = await postUrl.post("/", post)
    return data.data
}

const usePostPostCreate = () => {
    const queryClient = useQueryClient()
    return useMutation({
    	//함수 시행시에 ,mutationFn 호출.
        mutationFn: (post: Post) => postPostCreate(post),
        //성공처리
        onSuccess: () => {
            queryClient.invalidateQueries({
                queryKey: ['posts']
            })
        }
    })
}
```
성공시에는, posts키값을 가지오 있는 query객체들을 invalidate해준다.

```javascript
import {useForm} from "react-hook-form";
import {PostFormValues} from "../types/PostFormValues.ts";
import usePostPostCreate from "../services/usePostCreate.ts";
import {useNavigate} from "react-router-dom";

const PostCreateView = () => {
    const navigate = useNavigate();
    const {isLoading,error, mutateAsync} = usePostPostCreate()
    const {register,handleSubmit} = useForm()
    const onSubmit = async (values: PostFormValues) => {
        const newPost = {
            title: values.title,
            content: values.content,
            category: values.category,
            image: values.image
        }
        console.log(newPost)
        await mutateAsync(newPost)
        navigate("/")
    }

    return (
        <div>
            <form onSubmit={handleSubmit(onSubmit)}>
                {isLoading && <h1>loading</h1>}
                {error && <h1>{error}</h1>}
                <input
                    type = "text"
                    placeholder= "title"
                    {...register("title", {required:true})}
                />
                <input
                    type = "text"
                    placeholder= "content"
                    {...register("content", {required:true})}
                />
                <input
                    type = "text"
                    placeholder= "category"
                    {...register("category", {required:true})}
                />
                <input
                    type = "text"
                    placeholder= "image"
                    {...register("image", {required:true})}
                />
                <input type= "submit"/>
            </form>
        </div>
    );
};

export default PostCreateView;
```

이런 방식으로, onSubmit을 시행시켜줬을때, mutation이 잘 시행되는지, newPost가 생성이되는지 확인을 할 수 있다.

작성자: Subin