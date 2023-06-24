# method_missing của OpenStruct

Phương pháp giúp OpenStruct dễ dàng gán các key bất kỳ vào instance
https://github.com/ruby/ostruct/blob/master/lib/ostruct.rb

```rb
private def method_missing(mid, *args) # :nodoc:
    len = args.length
    if mname = mid[/.*(?==\z)/m]
      if len != 1
        raise! ArgumentError, "wrong number of arguments (given #{len}, expected 1)", caller(1)
      end
      set_ostruct_member_value!(mname, args[0])
    elsif len == 0
      @table[mid]
    else
      begin
        super
      rescue NoMethodError => err
        err.backtrace.shift
        raise!
      end
    end
  end
```
