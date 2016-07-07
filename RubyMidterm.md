# Ruby中間試験 ~実践的プログラミング~

## はじめに

試験ですが演習と同じです。何を使っても他人と相談してもTAに助けてもOKです。出来る問題だけではなく、完答を目指しましょう。
問題多くは、Rubyの資料を参考に出題しています。https://misoton665.gitbooks.io/rubytutorial-for-sccp2016/content/index.html

## 問題提出方法

- この試験の問題用紙をgitコマンドを利用して、自分のワークステーションにcloneしましょう。
- cloneしてきた後に出来上がったディレクトリに移動し、 *$ rm -rf .git* をタイプしましょう。
- emacsなどのお好みのエディタで試験用紙(ruby-midterm.md)に解答を書き込みましょう。
-  以下のリンクからリモートリポジトリを作成し、試験用紙をpushしましょう。
    - https://classroom.github.com/assignment-invitations/d4f70626782f6415b2c8854d2558679c
- 以上の操作はGitの講義内容を思い出して、実行しましょう
    - https://romtin.gitbooks.io/gittutorial-for-sccp2016/content/
    - https://github.com/SCCP2016/Document_git-tutorial-for-sccp2016/raw/master/slide4git_lecture.pptx
    - https://github.com/SCCP2016/Document_git-tutorial-for-sccp2016/raw/master/slide4git_exercise.pptx

## 1. 適切なプログラムを書け

標準出力に Hello World と出力するRubyのプログラムを書け。

```ruby
puts "Hello World"

```

## 2. 適切なものを選び、説明を埋めよ

次のうち、Rubyに存在しない型はどれか? また、存在する型について具体的な値を書け。
*Fixnum*, *Bignum*, *Float*, *Bool*, *String*

```
# 存在しない型
Bool
# 存在する型と具体例
# [答え方の例]
# 型: 具体例

Fixnum: 123
Bignum: 10000000000000000000
Float: 1.2
String: "Hello World"
```

## 3. 適切なプログラムを書け

映画館の金額を算出するプログラムを以下に示す仕様を満たして作成せよ。

- 小学生(12歳)以下は、700円
- 高校生(18歳)以下は、1000円
- 大学生(22歳)以下は、1200円
- 大人は、1500円
- 今日はレディースデー 全年齢の女性を対象とし、元の金額から200円引きとする
- 標準入力から２つの整数を受け取る
- ２つの整数はそれぞれ、 年齢 性別 (age sex) とする 
- 性別は、0:男性 1:女性 とする
- 入力に対して、金額を整数で出力する
- 出力をする命令は一度しか使ってはならない


```ruby
# 入力例1
# 12 0
# 出力例 1
# 700
# 入力例2
# 19 1
# 出力例2
# 1000

age, sex = STDIN.gets.split.map(&:to_i)
puts  case age
      when 0..12
        700
      when 12..18
        1000
      when 18..22
        1200
      else
        1500
      end - if sex==1 then 200 else 0 end
```

## 4. 適切なプログラムを書け

一つの文字列を標準入力より受け取り、以下の項目を標準出力に表示せよ。

- そのまま表示
- 文字数を表示
- 逆順にして表示 
- 全て大文字にして表示 
- 頭文字と末尾文字を削除して残りの文字列を表示
- アルファベットのa, b, c を大文字, その他のアルファベットや数字・記号はそのまま表示

```ruby
# 入力例
# ab5?cd
# 出力例
#ab5?cd
#6
#dc?5ba
#AB5?CD
#b5?c
#AB?Cd

dat = STDIN.gets.chomp
puts dat
puts dat.length
puts dat.reverse
puts dat.upcase
puts dat.slice(1,dat.length-2)
puts dat.tr("abc","ABC")
```

## 5. 適切なプログラムを書け

任意の数の整数の数列を受け取り、それらの最小値、最大値、合計値を求め表示せよ。
ただし、それぞれの値を求めるための関数を定義すること。

```ruby
# 入力例
# 10 1 5 4 17
# 出力例
# 1 17 37

def min(x)
  x.inject{|min,item| if min>item then item else min end }.to_s
end

def max(x)
  x.inject{|max,item| if max<item then item else max end }.to_s
end

def total(x)
  x.inject{|sum,item| sum +item}.to_s
end

i=STDIN.gets.split.map(&:to_i)
puts min(i)+" "+max(i)+" "+total(i)

```

## 6. 適切なプログラムを書け

標準入力から任意の文字列と整数を受け取り、以下の仕様を満たしたディレクトリを生成せよ(実際に実行し試せ)。

```
[入力例]
dir 3

[出来上がったディレクトリ]
$ ls
dir1/ dir2/ dir3/
```

- 作られるディレクトリのパーミッションは、
    - 奇数番号の場合は、 drwx---r-x
    - 偶数番号の場合は、 drwxr-xr--

とする。コメントにパーミッションの意味も書け。

ディレクトリ作成には、次の命令を使え。
http://docs.ruby-lang.org/ja/2.1.0/method/Dir/s/mkdir.html 

```ruby
name,val=STDIN.gets.split

for i in 1..val.to_i
  if i%2==1 then
    Dir.mkdir(name+i.to_s,0705)
  else
    Dir.mkdir(name+i.to_s,0754)
  end
end

# パーミッションについて
# drwxrwxrwx
# 最初のdはディレクトリを表す。
# その次の３つは自分、その次の３つは自分と同じグループのユーザ、
# その次の３つは他人の権限を表す。
# r、w、xはそれぞれ読み込み、書き込み、実行の権限を意味する。
# ディレクトリは移動するためには実行権限も必要。
```

## 7. 適切なプログラムを書け

暗号を解いて答えの文字列を表示するプログラムを書け。答えのキーワードは、コメントに記述せよ。
暗号は以下に示す表を使うことで複合することが出来る。
今回対象となる暗号は、"lymmkuknidpbruimyjkk" である。

```
"q" -> "e"
"t" -> "p"
"b" -> "b"
"n" -> "w"
"j" -> "s"
"u" -> "t"
"w" -> "z"
"c" -> "v"
"k" -> "i"
"d" -> "r"
"p" -> "u"
"h" -> "q"
"x" -> "m"
"z" -> "x"
"v" -> "h"
"l" -> "k"
"s" -> "j"
"i" -> "a"
"f" -> "d"
"r" -> "y"
"a" -> "c"
"m" -> "n"
"e" -> "f"
"y" -> "o"
"g" -> "g"
"o" -> "l"
```

```ruby

```

## 8. 適切なプログラムを書け

あなたはいかなる男女のペアでも結婚させられる能力を持っている。あまりにも要望が多いため、手続きを自動化したいと考えたあなたは、たくさんの結婚前の男女の名前から結婚後苗字の変わった女性の名前を生成するプログラムを初めに作ることにした。以下の入力例、出力例を見てそのプログラムを作成せよ。ただし、結婚できずに余った者に関しては出力してはならない。

入力は一行目に男性の名前列、二行目に女性の名前列が与えられ、左から順にペアを作って名前を生成していく。
それぞれの名前列で名前の数が異なる場合は少ない方に合わせてペアを作らなければならない。

入力
```
M1 M1 M3 ... Mn
W1 W2 W3 ... Wm
```

出力
```
O1 O2 O3 ... Oz
```
ここでzはn, mの内小さい方の数
```
# 入力例
SuzukiMakoto OgataRyo TanakaMichael TanakaTaro
KobayashiSaki AizuMisaki ShibuyaRin

# 出力例
SuzukiSaki OgataMisaki TanakaRin
```

```ruby
```

