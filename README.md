# プロを目指す人のためのRuby入門

4.7.6 配列を展開して「複数の引数」として渡したいとき(p119)

    a = []
    b = [2, 3]
    a.push(1) #=> [1]
    a.push(b) #=> [1, [2, 3]]

splat展開

    a = []
    b = [2, 3]
    a.push(1) #=> [1]
    a.push(*b) #=> [1, 2, 3]



4.7.13 配列の初期化について(p123)

    a = Array.new(5, 'default')
    a #=> ["default","default", "default", "default", "default"]
    
    
    str = a[0]
    str #=> "default"
    
    str.upcase!
    str #=> "DEFAULT"
    
    a #=> ["DEFAULT", "DEFAULT", "DEFAULT", "DEFAULT", "DEFAULT"]


    a = Array.new(5) { 'default' }
    a #=> ["default","default", "default", "default", "default"]
    
    str = a[0]
    str #=> "default"
    
    str.upcase!
    str #=> "DEFAULT"
    
    a #=> ["DEFAULT","default", "default", "default", "default"]



4.8.4 配列がブロック引数に渡される場合(p127)

    dimensions = [
      # [縦, 横]
      [10, 20],
      [30, 40],
      [50, 60],
    ]
    areas = []
    dimensions.each do |dimension|
      length = dimension[0]
      width = dimension[1]
      areas << length * width
    end
    areas #=> [200, 1200, 3000]


    dimensions = [
      # [縦, 横]
      [10, 20],
      [30, 40],
      [50, 60],
    ]
    areas = []
    dimensions.each do |length, width|
      areas << length * width
    end
    areas #=> [200, 1200, 3000]


4.10.3 繰り返し処理で使うbreakとreturnの違い(p141)

break => 繰り返し処理からの脱出
return => （繰り返し処理のみならず）メソッドからの脱出



5.2.2 ハッシュを使った繰り返し処理(p149)
    currencies = { 'japan' => 'yen', 'us' => 'dollar', 'india' => 'rupee' }
    
    currnecies.each do |key, value|
      puts "#{key}: #{value}"
    end
    #=> japan : yen
    #   us : dollar
    #   india: ruppee


    currencies = { 'japan' => 'yen', 'us' => 'dollar', 'india' => 'rupee' }
    
    currencies.each do |key_value|
      key = key_value[0]
      value = key_value[1]
      puts "#{key}": "#{value}"
    end
    #=> japan : yen
    #   us : dollar
    #   india: ruppee


5.4.3 メソッドのキーワード引数とハッシュ(p154)

2つ目と3つ目の引数が何を表しているのか、パッと分からない

    def buy_burger(menu, drink, potato)
      if drink
      end
      if potato
      end
    end
    
    buy_burger('cheese', true, true)
    buy_burger('cheese', true, false)

メソッドのキーワード引数を使うと可読性が上がる

    def buy_burger(menu, drink: true, potato: true)
    
    end
    
    buy_burger('cheese', drink: true, potato: true)
    buy_burger('cheese', drink: true, potato: false)


5.6.2 **でハッシュを展開させる(p163)
    h = { us: 'dollar', india: 'rupee' }
    { japan: 'yen', **h } #=> {:japan=>"yen", :us=>"dollar", :india=>"rupee"}
    
    { japan: 'yen', h } #=> error

上のコードの**のかわりにmergeメソッドで代替できる

    h = { us: 'dollar', india: 'rupee' }
    { japan: 'yen' }.merge(h) #=> {:japan=>"yen", :us=>"dollar", :india=>"rupee"}


5.6.4 任意のキーワードを受け付ける**引数(p164)

キーワード引数を使うメソッドに存在しないキーワードを渡すとエラーが発生する

    def buy_burger(menu, drink: true, potato: true)
      
    end
    
    buy_burger('fish', drink: true, potato: false, salad: true, chicken: false)
    #=> ArgumentError: unknown keywords: salad, chicken

**をつけた引数にはキーワード引数で指定されていないキーワードがハッシュとして格納される

    def buy_burger(menu, drink: true, potato: true, **others)
      
    end
    
    buy_burger('fish', drink: true, potato: false, salad: true, chicken: false)
    #=> {:salad=>true, :chicken=>false}


5.6.7 ハッシュから配列へ、配列からハッシュへ(p167)

注：キーが重複した場合は最後に登場した配列の要素がハッシュの値に採用される

    array = [[:japan, "yen"], [:japan, "円"]]
    array.to_h #=> {:japan=>"円"}

キーと値のペアの配列をHash[]に渡す

    array = [[:japan, "yen"], [:us, "dollar"], [:india, "rupee"]]
    Hash[array] #=> {:japan=>"yen", :us=>"dollar", :india=>"rupee"}

キーと値が交互に並ぶフラットな配列をsplat展開

    array = [:japan, "yen", :us, "dollar", :india, "rupee"]
    Hash[*array] #=> {:japan=>"yen", :us=>"dollar", :india=>"rupee"}


7.7.2 privateメソッド

privateメソッドは「レシーバを指定して呼び出すことができないメソッド」
privateメソッドではself付きで呼び出すとエラーになる。なぜならselfというレシーバをしてしてメソッドを呼び出したことになるから。


