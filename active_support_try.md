# Cách mà phương thức try trong rails được viết

https://github.com/rails/rails/blob/v7.0.5/activesupport/lib/active_support/core_ext/object/try.rb

```rb
module ActiveSupport
  module Tryable # :nodoc:
    def try(*args, &block)
      if args.empty? && block_given?
        if block.arity == 0
          instance_eval(&block)
        else
          yield self
        end
      elsif respond_to?(args.first)
        public_send(*args, &block)
      end
    end
    ruby2_keywords(:try)

    def try!(*args, &block)
      if args.empty? && block_given?
        if block.arity == 0
          instance_eval(&block)
        else
          yield self
        end
      else
        public_send(*args, &block)
      end
    end
    ruby2_keywords(:try!)
  end
end
```
