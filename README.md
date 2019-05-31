
# Hello World

# Pattern Matching
list = [1,2, [3,4,5]]
[a,b,c] = list

list
list = [1,2,3]
[a,2,b] = list

list = [1,2,3]
[a,1,b] = list

# Which will match?
a = [1,2,3]
a = 4
4 = a
[a,b] = [1,2,3]
a = [[1,2,3]]
[a] = [[1,2,3]]
[[a]] = [[1,2,3]]
[1, _, _] = [1,2,3]
[1, _, _] = [1,"cat","dog"]

# Ignoring a value with underscore
[1, 2, 3] = [a,b,c]
[1, _, _] = [1,"cat","dog"]

# Variables bind once (per match)
[a,a] = [1,1]
a
[a,a] = [1,2]

a = 1
[1, a, 3] = [1,2,3]

# Forcing an existing value
a = 1
a = 2
^a = 1

a = 1
[^a, 2] = [1,2]
a = 2
[^a, 2] = [1,2]

# Which will match
[a,b,a] = [1,2,3]
[a,b,a] = [1,1,2]
[a,b,a] = [1,2,1]

a = 2
[a,b,a] = [1,2,3]
a = 2
[a,b,a] = [1,1,2]
a = 2
a = 1
a = 2
^a = 2
a = 2
^a = 1
^a = 2 - a

# Immutable Data

#Using head tail to create a copy of list. 
list1 = [3,2,1]
list2 = [4 | list1]

name = "elixir"
cap_name = String.capitalize name

# Regex 
iex> Regex.run ~r{[aeiou]}, "caterpillar"
["a"]
iex> Regex.scan ~r{[aeiou]}, "caterpillar"
[["a"], ["e"], ["i"], ["a"]]
iex> Regex.split ~r{[aeiou]}, "caterpillar"
["c", "t", "rp", "ll", "r"]
iex> 

# Tuples
{1,2} 
{:ok,  42, "next"}
{:error, :enoent} 

{status, count, action} = {:ok, 42, "next"}

status
count
action

{status, file} = File.open("Rakefile")

{:ok, file} = File.open("Rakefile")
{:error, reason} = File.open("Rakefilenotthere")

# Lists
[1,2,3] ++ [4,5,6] # concatenation
[1,2,3,4] -- [2,4] # difference
1 in [1,2,3,4] # membership
"wombat" in [1,2,3,4]

# Keyword Lists
[ name: "Mike", city: "San Francisco", likes: "Programming Elixir" ]


DB.save record, [{:use_transaction, true}, {:logging, "HIGH"}]
DB.save record, use_transaction: true, logging: "HIGH"

[1, fred: 1, dave: 2]
{1, fred: 1, dave: 2}

# Maps
%{ key => value, key => value }

# Map with strings
states  = %{"AL" => "Alabama", "WI" => "Wisconsin"}

# Map with tuples
responses = %{{ :error, :enoent} => :fatal, {:error, :busy} => :retry}

# Map with atoms (?)
colors = %{ :red => 0xff0000, :green => 0x0ff00, :blue => 0x0000ff }

%{ "one" => 1, :two => 2, {1,1,1} => 3}

colors = %{ red: 0xff0000, green: 0x0ff00, blue: 0x0000ff }

# Accessing a map
states = %{ "AL" => "Alabama", "WI" => "Wisconsin"}
states["AL"]
states["TX"]

response_types = %{{ :error, :enoent} => :fatal, {:error, :busy} => :retry}
response_types[{:error, :busy}]

# Accessing a map with atoms
colors = %{ :red => 0xff0000, :green => 0x0ff00, :blue => 0x0000ff } 
colors[:red]
colors.green

# Binaries
bin = <<1, 2>>
byte_size bin
bin = <<3 :: size(2), 5:: size(4), 1 :: size(2)>>
:io.format("~-8.2b~n", :binary.bin_to_list(bin))
byte_size bin

# Anonymous Functions
sum = fn (a, b) -> a + b end
sum.(1,2)

greet = fn -> IO.puts "Hello" end
greet.()

f1 = fn a, b -> a * b end
f1.(5,6)

f2 = fn -> 99 end
f2.()

# Functions and Pattern Matching
iex> swap = fn {a,b} -> {b, a} end
#Function<6.128620087/1 in :erl_eval.expr/5>
iex> swap.({6,8})
{8, 6}

# My Turn
list_concat = fn (a,b) -> a ++ b end
list_concat.([:a, :b], [:c, :d])

sum = fn (a,b,c) -> a + b + c end
sum.(1,2,3)

pair_tuple_to_list = fn {a,b} -> [a + b] end
pair_tuple_to_list.({1234, 5678})

# One Function, Multiple Bodies
handle_open = fn 
  {:ok, file} -> "Read data: #{IO.read(file, :line)}"
  {_, error} -> "Error: #{:file.format_error(error)}"
end
handle_open.(File.open("hello.exs"))
handle_open.(File.open("nonexistent"))

**handle_open.exs**
handle_open = fn 
  {:ok, file} -> "Read data: #{IO.read(file, :line)}"
  {_, error} -> "Error: #{:file.format_error(error)}"
end
IO.puts handle_open.(File.open("hello.txt"))
IO.puts handle_open.(File.open("nonexistent"))

# FizzBuzz
```elixir
fizz_buzz = fn
  (0, 0, _) -> "FizzBuzz"
  (0, _, _) -> "Fizz"
  (_, 0, _) -> "Buzz"
  (_, _, a) -> a
end
fizz_buzz.(0,0)
fizz_buzz.(rem(10,3), rem(10,5), 10)
fizz_buzz.(rem(11,3), rem(11,5), 11)
fizz_buzz.(rem(12,3), rem(12,5), 12)
fizz_buzz.(rem(13,3), rem(13,5), 13)
fizz_buzz.(rem(14,3), rem(14,5), 14)
```

fizz_buzz_rem = fn n ->
  fizz_buzz.(rem(n,3), rem(n,5), n)
end
fizz_buzz_rem.(10)
fizz_buzz_rem.(11)
fizz_buzz_rem.(12)
fizz_buzz_rem.(13)
fizz_buzz_rem.(14)
fizz_buzz_rem.(15)
fizz_buzz_rem.(16)
fizz_buzz_rem.(17)

[http://wiki.c2.com/?FizzBuzzTest](http://wiki.c2.com/?FizzBuzzTest)

# Functions Can Return Functions
fun1 = fn -> fn -> "Hello" end end
fun1.()
fun1.().()

fun1 = fn ->
  fn -> 
    "Hello"
  end
end

fun1 = fn -> (fn -> "hello" end) end
other = fun1.()
other.()

# Functions Remember Their Original Environment
greeter = fn name -> (fn -> "Hello #{name}" end) end
mike_greeter = greeter.("Mike")
mike_greeter.()

# Parameterized Functions
add_n = fn n -> (fn other -> n + other end) end
add_two = add_n.(2)
add_five = add_n.(5)
add_two.(3)
add_five.(7)

# My turn
prefix = fn str -> (fn other -> "#{str} #{other}" end) end
mrs = prefix.("Mrs")
mrs.("Smith")
prefix.("Elixir").("Rocks")


# Passing Functions as Arguements
times_2 = fn n -> n * 2 end
apply = fn (fun, value) -> fun.(value) end
apply.(times_2, 6)

# Enum has a built in function called map. It takes two arguments: a collection and  a function.
# It returns a list that is the result of applying that function to each element of the collection.
list = [1,3,5,7,9]
Enum.map list, fn elem -> elem * 2 end
Enum.map list, fn elem -> elem * elem end
Enum.map list, fn elem -> elem > 6 end

# Pinned Values and Function Parameters
```elixir
defmodule Greeter do
  def for(name, greeting) do
    fn 
      (^name) -> "#{greeting} #{name}"
      (_)     -> "I don't know you"
    end 
  end
end

mr_valim = Greeter.for("Jose", "Oi!")
IO.puts mr_valim.("Mike")
IO.puts mr_valim.("Mike")
```

# The & Noation
add_one = &(&1 + 1)
add_one.(44)
square = &(&1 * &1)
square.(8)

speak = &(IO.puts(&1))
speak.("Hello")

rnd = &(Float.round(&1, &2))
rnd = &(Float.round(&2, &1))

divrem = &{ div(&1, &2), rem(&1, &2) }
divrem.(13, 5)

s = &"bacon and #{&1}"
s.("custard")


match_end = &~r/.*#{&1}$/
"cat" =~ match_end.("t")
"cat" =~ match_end.("!")

l = &length/1
l.([1,2,3,4])

len = &Enum.count/1
len.([1,2,3,4])

m = &Kernel.min/2
m.(99,88)

Enum.map [1,2,3,4], &(&1 + 1)
Enum.map [1,2,3,4], &(&1 < 3)

# My turn
Enum.map [1,2,3,4], fn x -> x + 2 end
Enum.map [1,2,3,4], &(&1 + 2)

Enum.each [1,2,3,4], fn x -> IO.inspect x end
Enum.each [1,2,3,4], &(IO.inspect &1)

# Modules and Named Functions
**mm/times.exs**
```elixir 
defmodule Times do
  def double(n) do
    n * 2
  end
end
```

iex times.exs
Times.double(4)

c "times.exs"
Times.double(4)
Times.double(123)

**mm/times1.exs**
```elixir
defmodule Times do
  def double(n) do: n * 2
end
```

## My turn
**mm/times3.exs**
```elixir
defmodule Times do (
  def double(n), do: n * 2
  def triple(n), do: n * 3
)
end
```

iex times3.exs
Times.triple(4)
Times.triple(123)

**mm/times4.exs**
```elixir
defmodule Times do (
  def double(n), do: n * 2
  def triple(n), do: n * 3
  def quadruple(n), do: double(n) * 2
)
end
```

iex times4.exs
Times.quadruple(4)
Times.quadruple(123)

## Function Calls and Pattern Matching

***mm/factorial1.exs***
```elixir
defmodule Factorial do
  def of(0), do: 1
  def of(n), do: n * of(n-1)
end
```

***mm/factorial1-bad.exs***
```elixir
defmodule BadFactorial do
  def of(n), do: n * of(n-1)
  def of(0), do: 1
end
```

```elixir
iex(1)> c "factorial1-bad.exs"
warning: this clause cannot match because a previous clause at line 2 always matches
  factorial1-bad.exs:3
```

# My turn
***mm/sum1.exs***
```elixir
defmodule Sum do
  def of(0), do: 0
  def of(n), do: n + of(n-1)
end
```

# Guard Clauses
***mm/guard.exs***
```elixir
defmodule Guard do
  def what_is(x) when is_number(x) do
    IO.puts "#{x} is a number"
  end
  def what_is(x) when is_list(x) do
    IO.puts "#{inspect(x)} is a list"
  end
  def what_is(x) when is_atom(x) do
    IO.puts "#{x} is a atom"
  end
end
Guard.what_is(99)
Guard.what_is(:cat)
Guard.what_is([1,2,3,4])
```

# Default Parameters
***default_params.exs***
```elixir
defmodule Example do
  def func(p1, p2 \\ 2, p3 \\ 3, p4) do
    IO.inspect [p1, p2, p3, p4]
  end
end

Example.func("a", "b")
Example.func("a", "b", "c")
Example.func("a", "b", "c", "d")
```

***default_params-bad.exs***
```elixir
defmodule Example do
  def func(p1, p2 \\ 2, p3 \\ 3, p4) do
    IO.inspect [p1, p2, p3, p4]
  end
  def func(p1, p2) do
    IO.inspect [p1, p2]
  end
end
```

```bash
== Compilation error in file default_params-bad.exs ==
** (CompileError) default_params-bad.exs:5: def func/2 conflicts with defaults from func/4
```

***default_params1.exs***
```elixir
defmodule DefaultParams1 do
  def func(p1, p2 \\ 123) do
    IO.inspect [p1, p2]
  end
  def func(p1, 99) do
    IO.puts "you said 99"
  end
end
```

```bash
warning: redefining module DefaultParams1 (current version defined in memory)
  default_params1.exs:1

warning: variable "p1" is unused (if the variable is not meant to be used, prefix it with an underscore)
  default_params1.exs:5

warning: def func/2 has multiple clauses and also declares default values. In such cases, the default values should be defined in a header. Instead of:

    def foo(:first_clause, b \\ :default) do ... end
    def foo(:second_clause, b) do ... end

one should write:

    def foo(a, b \\ :default)
    def foo(:first_clause, b) do ... end
    def foo(:second_clause, b) do ... end

  default_params1.exs:5

warning: this clause cannot match because a previous clause at line 2 always matches
  default_params1.exs:5

[DefaultParams1]
```

***mm/default_params2.exs***
```elixir
defmodule Params do
  def func(p1, p2 \\ 123)

  def func(p1, p2) when is_list(p1) do
    "You said #{p2} with a list"
  end
  def func(p1, p2) do
    "You passed in #{p1} and #{p2}"
  end
end

IO.puts Params.func(99)
IO.puts Params.func(99, "cat")
IO.puts Params.func([99])
IO.puts Params.func([99], "dog")
```

# My turn
***exercises/ModulesAndFunctions-6.exs***
```elixir
defmodule Chop do
  def middle(min, max), do: div(min + max, 2)

  def guess(number, low..high) when div(low + high, 2) > number do
    IO.puts "Is it #{middle(low, high)}"
    guess(number, low..middle(low, high))
  end

  def guess(number, low..high) when div(low + high, 2) < number do
    IO.puts "Is it #{middle(low, high)}"
    guess(number, middle(low, high)..high)
  end

  def guess(number, low..high), do: IO.puts middle(low, high)
end

IO.puts(Chop.guess(273, 1..1000))
```

# Private Functions

# Pipe Operator
```elixir
(1..10) |> Enum.map(&(&1*&1)) |> Enum.filter(&(&1 < 40))
```

# Modules
```elixir
defmodule Mod do
  def func1 do
    IO.puts "in func1"
  end
  def func2 do
    func1()
    IO.puts "in func2"
  end
end
Mod.func1
Mod.func2
```

```elixir
defmodule Outer do
  defmodule Inner do
    def inner_func do
      IO.puts "inner_func"
    end
  end
  def outer_func do
    Inner.inner_func
  end
end
Outer.outer_func
Outer.Inner.inner_func
```

```elixir
defmodule Mix.Tasks.Doctest do
  def run do
    IO.puts "doc test"
  end
end
Mix.Tasks.Doctest
```

# Import Directive
```elixir
defmodule Example do
  def func1 do
    List.flatten [1,[2,3],4]
  end
  def func2 do
    import List, only: [flatten: 1]
    flatten [5,[6,7],8]
  end
end
```

# Alias Directive
```elixir
defmodule Example do
  def compile_and_go(source) do
    alias My.Other.Module.Parser, as: Parser
    alias My.Other.Module.Runner, as: Runner
    source
    |> Parser.parse()
    |> Runner.execute()
  end
end
```

```elixir
    alias My.Other.Module.Parser
    alias My.Other.Module.Runner
```

```elixir
    alias My.Other.Module.{Parser, Runner}
```

# Module Attributes
***
```elixir
defmodule Example do
  @author "Michael Chavez"
  def get_author do
    @author
  end
end
IO.puts "Example was written by #{Example.get_author}"
```

# Module Names: Elixir, Erlang, and Atoms
```elixir
is_atom IO
```

```elixir
to_string IO
```

```elixir
:"Elixir.IO" === IO
```

```elixir
IO.puts 123
```

```elixir
:"Elixir.IO".puts 123
```

```elixir
my_io = IO
```

```elixir
my_io.puts 123
```










