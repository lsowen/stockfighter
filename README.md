# stockfighter-io-trades

A Python3 library for the Stockfighter Trades.Exec() API.

## Usage

### Local Project Install

This will install it in your project:

    git clone https://github.com/karma0/stockfighter-io-trades.git sf
    ln -s sf/stockfighter-io-trades .
    cp sf/config.py.example sf/config.py

### PyPi Install

Execute, then continue with configuration:

    pip install stockfighter-io-trades

## Configuration

Create your configuration using the config.py.example in the root of this project as an example, or copy it to `config.py`, and proceed with the following:

1. Set your `apikey` and `gm_apikey` to the correct values associated with your account.  The `gm_apikey` can be found in the cookies while you're logged in on the site.

2. Set your levelInstance variables.  You can find them by browsing (here)[https://www.stockfighter.io/ui/levels].

3. `from sf.config import *` This will initialize a `CONF` variable that you can pass around with class initializers.  This will also come with a `DEFCONF` variable that will allow you to use the TESTEX exchange, allowing you to go back and forth using different instantiated objects.


## Execution

### Start a game

    from stockfighter-io-trades.api.game import *
    from stockfighter-io-trades.config import *
    g = Game(CONF, 'sell_side')
    g.start_level()

### Interact with an exchange

    from stockfighter-io-trades.exchange import Market

    m = Market(CONF)
    q = m.quote()

Output will be:

    {
      'ok': True,
      'venue': 'TESTEX',
      'symbol': 'FOOBAR',
      'ask': 65535,
      'askDepth': 15087,
      'askSize': 15087,
      'bid': 50,
      'bidDepth': 3152,
      'bidSize': 2490,
      'last': 50,
      'lastSize': 100,
      'lastTrade': '2015-12-16T23:07:05.24319087Z',
      'quoteTime': '2015-12-16T23:10:48.09910821Z'
    }

### API

#### Market.api_is_up()

Returns `True` or `False`.

#### Market.venue_is_up()

Returns `True` or `False`.

#### Market.stocks()

Returns a list of stocks from the exchange.

#### Market.orderbook()

Returns the order book.

#### Market.quote()

Returns a quote for the given stock.

#### Market.ask(cost, quantity, direction="sell", order_type='limit')

Pass in:

* _cost_: price you're asking for
* _quantity_: how many you want to buy
* _direction_ (optional): "buy" or "sell" (allows for generic call to `order`)
* _order_type_ (optional): may be 'limit', 'market', 'fill-or-kill', or 'immediate-or-cancel'. Default: 'limit'

Returns the (order object)[https://starfighter.readme.io/docs/place-new-order].

#### Market.bid(cost, quantity, order_type='limit')

* _cost_: price you're asking for
* _quantity_: how many you want to buy
* _order_type_ (optional): may be 'limit', 'market', 'fill-or-kill', or 'immediate-or-cancel'. Default: 'limit'

Returns the (order object)[https://starfighter.readme.io/docs/place-new-order].

#### Market.status(order_id)

Pass in:

* _order_id_: The id passed back from in the (order object)[https://starfighter.readme.io/docs/place-new-order].

Returns an updated copy of the (order object)[https://starfighter.readme.io/docs/place-new-order].

#### Market.cancel(order_id)

Pass in:

* _order_id_: The id passed back from in the (order object)[https://starfighter.readme.io/docs/place-new-order].

Returns an updated (and final) copy of the (order object)[https://starfighter.readme.io/docs/place-new-order].

## Contributing

Please issue a pull request.

## Support

Please submit questions as an issue to get a prompt response.
