# Giới thiệu về Storybook cho dự án Frontend

## Storybook là gì?

Storybook là một công cụ mã nguồn mở giúp phát triển và thiết kế các UI component một cách độc lập trong môi trường biệt lập. Nó cho phép bạn xây dựng, kiểm tra và tài liệu hóa các component UI mà không cần phải chạy toàn bộ ứng dụng.

Ví dụ: Bạn đang phát triển một nút (button) component. Với Storybook, bạn có thể:

1. Tạo các biến thể khác nhau của nút (kích thước, màu sắc, trạng thái)
2. Xem tất cả các biến thể cùng một lúc
3. Tương tác với nút để kiểm tra chức năng
4. Tự động tạo tài liệu cho component

Tất cả điều này được thực hiện trong một môi trường riêng biệt, không ảnh hưởng đến ứng dụng chính của bạn.

## Tại sao cần sử dụng Storybook?

1. **Phát triển component-driven**: Tập trung vào từng component riêng lẻ trước khi tích hợp vào ứng dụng.

2. **Kiểm tra trực quan**: Dễ dàng kiểm tra giao diện và chức năng của component trong các trường hợp khác nhau.

3. **Tài liệu sống**: Tự động tạo tài liệu cho các component, giúp team dễ dàng hiểu và sử dụng.

4. **Cộng tác hiệu quả**: Designers và developers có thể làm việc cùng nhau trên các component.

5. **Tái sử dụng code**: Khuyến khích việc tạo ra các component có thể tái sử dụng.

## Cách Storybook hoạt động

Storybook chạy song song với ứng dụng của bạn. Mỗi component được định nghĩa như một "story" - một trạng thái cụ thể của component đó.

Ví dụ về một story đơn giản cho một Button component:

```javascript
import React from "react";
import { Button } from "./Button";

export default {
  title: "Components/Button",
  component: Button,
};

export const Primary = () => <Button primary>Primary Button</Button>;
export const Secondary = () => <Button>Secondary Button</Button>;
export const Large = () => <Button size="large">Large Button</Button>;
```

Trong ví dụ này:

- Chúng ta định nghĩa 3 stories cho Button component: Primary, Secondary, và Large.
- Mỗi story hiển thị Button trong một trạng thái cụ thể.

## Cài đặt và sử dụng Storybook

1. Cài đặt Storybook trong dự án React của bạn:

```bash
npx sb init
```

2. Chạy Storybook:

```bash
npm run storybook
```

3. Truy cập Storybook UI tại http://localhost:6006

## Ví dụ thực tế: Todo List Component

Hãy xem xét một ví dụ phức tạp hơn với một Todo List component:

```javascript
// TodoList.stories.js
import React from "react";
import { TodoList } from "./TodoList";

export default {
  title: "Components/TodoList",
  component: TodoList,
};

const Template = (args) => <TodoList {...args} />;

export const EmptyList = Template.bind({});
EmptyList.args = {
  items: [],
};

export const WithItems = Template.bind({});
WithItems.args = {
  items: [
    { id: 1, text: "Buy groceries", completed: false },
    { id: 2, text: "Walk the dog", completed: true },
    { id: 3, text: "Do laundry", completed: false },
  ],
};

export const AllCompleted = Template.bind({});
AllCompleted.args = {
  items: [
    { id: 1, text: "Buy groceries", completed: true },
    { id: 2, text: "Walk the dog", completed: true },
    { id: 3, text: "Do laundry", completed: true },
  ],
};
```

Trong ví dụ này:

- Chúng ta tạo ra 3 stories cho TodoList component: EmptyList, WithItems, và AllCompleted.
- Mỗi story hiển thị TodoList trong một trạng thái khác nhau.
- Chúng ta sử dụng Template và args để dễ dàng tạo ra các biến thể khác nhau của component.

## Lợi ích của Storybook

1. **Phát triển nhanh chóng**: Bạn có thể phát triển và kiểm tra các component mà không cần chạy toàn bộ ứng dụng.

2. **Kiểm tra dễ dàng**: Bạn có thể kiểm tra các trạng thái khác nhau của component một cách nhanh chóng.

3. **Tài liệu tự động**: Storybook tự động tạo tài liệu cho các component của bạn.

4. **Cộng tác hiệu quả**: Designers và developers có thể làm việc cùng nhau trên các component.

5. **Tái sử dụng code**: Khuyến khích việc tạo ra các component có thể tái sử dụng.

6. **Tích hợp với các công cụ khác**: Storybook có thể tích hợp với nhiều công cụ khác như Jest cho unit testing, Figma cho design, v.v.

Với Storybook, bạn có thể xây dựng một thư viện component mạnh mẽ và dễ quản lý, giúp tăng tốc quá trình phát triển và cải thiện chất lượng code của dự án frontend của bạn.
