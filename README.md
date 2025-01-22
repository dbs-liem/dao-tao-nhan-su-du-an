# Đào tạo nhân sự mới cho dự án Precision
# Mục lục

[I. Quy trình đào tạo nhân sự mới](#i-quy-trình-đào-tạo-nhân-sự-mới)
- [1. Những việc cần làm](#1-những-việc-cần-làm)
- [2. Những việc không cần và không nên làm](#2-những-việc-không-cần-và-không-nên-làm)

[II. Best practices with VueJS](#ii-best-practices-with-vuejs)
- [1. Luôn sử dụng :key với v-for directive](#1-luôn-sử-dụng-key-với-v-for-directive)
- [2. Khai báo props với camelCase và kebab-case cho templates](#2-khai-báo-props-với-camelCase-và-kebab-case-cho-templates)
- [3. Sử dụng kebab-case cho events](#3-sử-dụng-kebab-case-cho-events)
- [4. Tránh sử dụng v-if với v-for](#4-tránh-sử-dụng-v-if-với-v-for)
- [5. Khi khai báo prop nên khai báo chi tiết nhất có thể](#5-khi-khai-báo-prop-nên-khai-báo-chi-tiết-nhất-có-thể)
- [6. Sử dụng PascalCase hoặc kebab-case cho components](#6-sử-dụng-PascalCase-hoặc-kebab-case-cho-components)
- [7. Sử dụng kiểu viết tắt (Use of Shorthands)](#7-sử-dụng-kiểu-viết-tắt-Use-of-Shorthands)
- [8. Không gọi method đồng thời trong created và watch](#8-không-gọi-method-đồng-thời-trong-created-và-watch)
- [9. Không nên sử dụng các biểu thức trong template](#9-không-nên-sử-dụng-các-biểu-thức-trong-template)
- [10. Gọi API trong action và commit data (Vuex)](#10-gọi-API-trong-action-và-commit-data-Vuex)
- [11. Sử dụng slot cho component](#11-sử-dụng-slot-cho-component)
- [12. Sử dụng mapState, mapGetters, mapMutations and mapActions](#12-sử-dụng-mapState-mapGetters-mapMutations-and-mapActions)

[III. Kết thúc](#iii-kết-thúc)

# I. Quy trình đào tạo nhân sự mới
## 1. Những việc cần làm
- **Đọc kĩ yêu cầu** của KH ( nếu có thắc mắc thì hỏi lại Thanh hoặc Thái )
- Xác định những **nơi cần lập trình**
- Xác định **mức độ ảnh hưởng** khi lập trình
- **Estimate** thời gian làm task (Nếu quá thời gian `4h/tuần` thì liên hệ lại với Team để sắp xếp)
- Bắt đầu **tạo nhánh** (ở dự án hiện tại)
  - Ở source `cds-app`:

    ```
    Task của ông Hino, Tanaka sẽ tạo từ staging và đặt tên là ft-xxxxxx
    Task của ông Naka thì tạo từ dev và đặt tên là dev-xxx
    ```
  - Ở source `cds-monshin-app-ver2` và `cds-pre-monshin-ver2`:

    ```
    Sẽ tạo từ develop và đặt tên là feature-xxxxxx
    ```
- Thực hiện **lập trình**
- Kiểm tra lại **code và push** code lên nhánh (Clean code)
  - Cách **commit code**:
    ```
    Nội dung của commit đầu tiên như sau:
    refs #xxxxxx tiêu đề task
    Những commit tiếp theo sẽ thực hiện như sau: 
    refs #xxxxxx nội dung chỉnh sửa của commit này
    ```
  - Ví dụ:
- Kiểm tra **kết quả**
- Tạo merge request **daft** và đưa **Thái** review code và test lại (Nếu review **OK** thì đi tiếp, còn **chưa** được thì chỉnh sửa lại và nhờ review lại)
- **Bỏ daft** ở merge request và trả task lại cho KH.
## 2. Những việc không cần và không nên làm
- **Không nên push hay commit code** lên nhánh nào khác ngoài nhánh đang thực hiện task
- Cố gắng **không tác động đến luồng code** của người khác
- Lưu ý **không tạo sai tên nhánh, merge request**
- Tránh **code xấu, tên biến vô nghĩa, những code dư thừa không sử dụng,** vì phía KH cũng sẽ review lại code
- Tránh **sửa đổi CSS liên quan đến những class chung hoặc class nhiều component sử dụng** (Quan trọng)

# II. Best practices with VueJS
## 1. Luôn sử dụng :key với v-for directive
- Thuộc tính này được sử dụng để kiểm tra tính duy nhất của từng mục trong danh sách. Virtual DOM của Vue tạo VNodes trên mỗi mục của danh sách. Vì vậy, nếu không có thuộc tính :key trong các mục danh sách thì Virtual DOM sẽ không xác định được từng mục là riêng biệt. Vì vậy, Virtual DOM sẽ khó phát hiện bất kỳ thay đổi nào đối với một mục danh sách cụ thể.
- Ví dụ:
  ```
  <template>
    <!-- BAD -->
    <div v-for="product in products">{{ product }}</div>
    
    <!-- GOOD! -->
    <div v-for="product in products" : key="product.id">{{ product }}</div>
  </template>
  ```

## 2. Khai báo props với camelCase và kebab-case cho templates
- Trong JavaScript, tiêu chuẩn đặt tên là `camelCase`, còn trong HTML, tiêu chuẩn đặt tên là `kebab-case`.
- Ví dụ:
  ```
  BAD!
    <template>
      <PopupWindow titleText "hello world" />
    </template>
    
    <script>
      export default {
        props: {
            'title-text': String
        }
      }
    </script>
    
  GOOD!
    <template>
      <PopupWindow title-text="hello world" />
    </template>

    <script>
      export default {
        props: {
            titleText: String
        }
      }
    </script>
  ```

## 3. Sử dụng kebab-case cho events
- Khi viết các custom event thì chúng ta nên sử dụng `kebab-case` vì khi lắng nghe lại event này ở component cha nó cũng ở dạng `kebab-case`. Vì vậy, để có sự nhất quán giữa các components và để làm cho code dễ đọc hơn, hãy sử dụng `kebab-case` ở cả hai nơi.
- Ví dụ:
   ```
  PopupWindow.vue
  this.$emit("close-window")

  ParentComponent.vue
  <popup-window @close-window='handleEvent()' />
  ```

## 4. Tránh sử dụng v-if với v-for
- **Đừng bao giờ đồng thời sử dụng `v-if và v-for` trên cùng một element**
- Khi Vue xử lý directives, `v-for` sẽ có mức độ ưu tiên cao hơn `v-if`.
- Có **hai** trường hợp phổ biến mà điều này có thể đáng chú ý:
  - Để lọc các mục trong danh sách (ví dụ: `v-for="user in users"` `v-if="user.isActive"`)
    - Trong những trường hợp này, hãy thay thế `users` bằng một computed property (ví dụ: `activeUsers`)
    - Ví dụ:
       ```
       BAD!
        <ul>
          <li 
            v-for="user in users'"
            v-if="user.isActive"
            :key="user.id">
            {{ user.name }}
          </li>
        </ul>

       GOOD!
        <ul>
          <li 
            v-for="user in activeUsers" 
            :key="user.id">
            {{ user.name }}
          </li>
        </ul>
       ```

  - Để tránh hiển thị danh sách nếu danh sách đó cần bị ẩn (ví dụ: `v-for="user in users"` `v-if="shouldShowUsers"`)
    - Trong những trường hợp này, hãy di chuyển `v-if` sang một phần tử cha (ví dụ: `ul`, `ol`)
    - Ví dụ:
       ```
       BAD!
        <ul>
          <li 
            v-for="user in users"
            v-if="shouldShowUsers"
            :key="user.id">
            {{ user.name }}
          </li>
        </ul>
  
       GOOD!
        <ul v-if="shouldShowUsers">
          <li 
            v-for="user in users" 
            :key="user.id">
            {{ user.name }}
          </li>
        </ul>
       ```

## 5. Khi khai báo prop nên khai báo chi tiết nhất có thể
- Nên `validate` dữ liệu của `props` ngay trong phần khai báo.
- Về cơ bản, nó giúp **bạn của tương lai** khỏi **bạn của hiện tại**.
- Khi ở trong một dự án quy mô lớn, bạn rất dễ quên chính xác định dạng, loại và các quy ước khác mà bạn đã sử dụng cho 1 `prop`.
- Và những người đến sau cũng sẽ **dễ dàng** hơn trong việc tìm hiểu và sử dụng components của bạn.
- Ví dụ:
   ```
   BAD!
     // This is only OK when prototyping
     props: ['status']

   GOOD!
     props: {
      status: String
     }

   Even Better Code!
    props: {
      status: {
        type: String, // Định nghĩa kiểu dữ liệu là String
        required: true, // Đánh dấu prop này là bắt buộc
        validator: function (value) { 
          // Kiểm tra giá trị của prop có thuộc danh sách hợp lệ không
          return ['syncing', 'synced', 'version-conflict', 'error'].indexOf(value) !== -1;
        }
      }
    }
   ```

## 6. Sử dụng PascalCase hoặc kebab-case cho components
- `PascalCase` hoạt động tốt nhất vì nó được hỗ trợ bởi hầu hết các tính năng tự động điền của `IDE`.
- Ví dụ:
   ```
   BAD!
     components/
     |- mycomponent.vue
     components/
     |- myComponent.vue

   GOOD!
     components/
     |- MyComponent.vue
     components/
     |- my-component.vue
   ```

## 7. Sử dụng kiểu viết tắt (Use of Shorthands)
- Có sự nhất quán trong việc sử dụng `directives shorthands` thay cho fullname.
- Ví dụ: 
   ```
    : is short for v-bind
    @ is short for v-on
    # is short for v-slot
   ```

## 8. Không gọi method đồng thời trong created và watch
- Một sai lầm phổ biến của lập trình viên Vue (dev) là gọi `method` đồng thời trong `created` và `watch` một cách không cần thiết.
- Ý nghĩa đằng sau điều này là muốn gọi `method` đó sau khi component được khởi tạo.
- Tuy nhiên, Vue đã có một giải pháp tích hợp sẵn cho việc này. Và tất cả những gì chúng ta cần làm là tái cấu trúc lại `watcher` một chút và khai báo **2 thuộc tính** sau:
  - `handler (newVal, oldVal)` – this is our watcher method itself
  - `immediate: true` – this makes our handler run when our instance is created
  - Ví dụ:
     ```
     BAD!
       created: () => {
          this.handleChange();
        },
        
        methods: {
          handleChange() {
            // stuff happens
          }
        },
        
        watch: {
          property() {
            this.handleChange();
          }
        }
  
     GOOD!
       methods: {
          handleChange() {
            // stuff happens
          }
        },
        
        watch: {
          property: {
            immediate: true,
            handler() {
              this.handleChange();
            }
          }
        }
     ```

## 9. Không nên sử dụng các biểu thức trong template
- Việc sử dụng nhiều biểu thức trong template khiến code trở nên **phức tạp và lộn xộn**. Vì vậy hãy làm cho template **đơn giản** hơn, thông qua việc sử dụng `computed`
- Ví dụ:
     ```
     BAD!
       <template>
        {{ fullName.split(' ').map(function (word) { 
          return word[0].toUpperCase() + word.slice(1); 
        }).join(' ') }}
       </template>
  
     GOOD!
       <template>
        {{ normalizedFullName }}
       </template>
      
       <script>
         export default {
           // The complex expression has been moved to a computed property
           computed: {
             normalizedFullName() {
               return this.fullName
                 .split(' ')
                 .map(word => word.charAt(0).toUpperCase() + word.slice(1))
                 .join(' ');
             }
           }
         }
       </script>
     ```

## 10. Gọi API trong action và commit data (Vuex)
- Sử dụng Vuex `actions` để thực hiện phần lớn các lệnh gọi API vì chúng giúp lấy dữ liệu **dễ dàng** hơn rất nhiều và cung cấp mức độ có thể **tái sử dụng** và **đóng gói**.
- Ví dụ nếu ở 2 trang mà call **cùng** 1 API thì chúng ta phải gọi lại API đó ở 2 page, dẫn đến **bị trùng lặp** code ở đây. Nếu bạn đã call api đó ở `action` thì chúng ta chỉ cần `dispatch action` đó là xong.
- Từ ví dụ trên chúng ta sẽ thấy **code logic** và **clear** hơn khi chúng ta biết API chúng ta gọi đang ở đâu.

  *Note: Hiện tại các dự án của Precision cũng đang sử dụng phương pháp này*

## 11. Sử dụng slot cho component
- `Slots` là các không gian được cung cấp bởi Vuejs để hiển thị nội dung được truyền từ **thành phần này** sang **thành phần khác**.
- Nổi bật qua việc làm cho các components của bạn có **thể tái sử dụng** và **dễ bảo trì hơn**
- Ở ví dụ dưới đây, component temp đang sử dụng component `componentSlot` và truyền nội dung qua 3 `slot` là **header**, **default** và **footer**

  ![image](https://github.com/user-attachments/assets/d3ec6ea0-4f53-44f3-a190-ec87bda268f4)

## 12. Sử dụng mapState, mapGetters, mapMutations and mapActions
- Thông thường khi cần truy cập `state`, `getters`, hay `dispatch action` trong một component ta cần tạo nhiều `computed properties` hoặc `methods`
- Nhưng thay vào đó sử dụng `mapState`, `mapGetters`, `mapMutations` and `mapActions` có thể giúp bạn **rút ngắn đoạn code** và làm mọi thứ **dễ hiểu hơn** bằng cách nhóm những gì đến từ các `store modules` vào một nơi

  ![image](https://github.com/user-attachments/assets/afd837e8-abf9-44e1-941f-64d1b4ec3d3b)

# III. Kết thúc
- *Mong rằng tài liệu này sẽ đồng hành cùng bạn trên con đường khám phá và ứng dụng những kiến thức mới. Chúc bạn không chỉ hiểu mà còn áp dụng thành công những gì đã học, để mỗi bước đi trong công việc và cuộc sống đều đầy tự tin và sáng tạo. Hãy luôn tiến về phía trước, không ngừng học hỏi và phát triển.* :stuck_out_tongue_winking_eye:

:pencil:: **Liêm King**
