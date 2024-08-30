# `FlexfillsApi`

The `FlexfillsApi` is a package for using Flex Fills WebSocket communication with FlexFills trading services.

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install FlexfillsApi.

```bash
pip install FlexfillsApi
```

## Usage

```python
import FlexfillsApi

# initialize FlexfillsApi, returns authenticated FlexfillsApi Object
flexfills_api = FlexfillsApi.initialize('username', 'password', is_test=True)

# get assets list
assets_list = flexfills_api.get_asset_list()

# get instruments list
assets_list = flexfills_api.get_instrument_list()
```

### Available Functions

<table class="table table-bordered">
    <thead class="thead-light">
        <tr>
            <th>Functions</th>
            <th>Params</th>
            <th>Explaination</th>
            <th>Response</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code class="highlighter-rouge">get_asset_list()</code></td>
            <td></td>
            <td>Provides a list of supported assets and their trading specifications.</td>
            <td>
                <code class="highlighter-rouge">
                {
                    "event": "GET",
                    "channel": "ASSET_LIST",
                    "data": [
                        {
                            "class": "Currency",
                            "code": "USC",
                            "name": null
                        },
                        ...
                    ]
                }
                </code>
            </td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">get_instrument_list()</code></td>
            <td></td>
            <td>Provides a list of supported Instruments and their trading specifications.</td>
            <td>
                <code class="highlighter-rouge">
                {
                    "event": "GET",
                    "channel": "INSTRUMENT_LIST",
                    "data": [
                        {
                            "class": "Instrument",
                            "quoteCurrencyCode": "BAT",
                            "code": "BAT/ETH",
                            "name": null
                        },
                        ...
                    ]
                }
                </code>
            </td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">subscribe_order_books(instruments)</code></td>
            <td><p>**instruments:** list of pair of currencies. All available pairs are:</p>
            <code class="highlighter-rouge">BTC/PLN, DASH/PLN, EUR/GBP, LTC/GBP, LTC/USD, OMG/EUR, OMG/PLN, USDT/EUR, XRP/USD, ZEC/BTC, ZEC/PLN, ZRX/BTC, DOT/BTC, ZRX/USD, BSV/USDT, ADA/USDT, ZIL/USDT, ENJ/USD, XEM/USDT, BNB/USDT, BSV/EUR, BTC/EUR, DASH/EUR, LINK/USD, LTC/ETH, ZEC/USD, BAT/USDT, DOT/USDT, DOT/ETH, MATIC/USTD, AVAX/USDT, BAT/EUR, BAT/GBP, BCH/BTC, BTC/USDT, ETH/GBP, EUR/USD, LINK/BTC, LINK/ETH, LTC/EUR, LTC/USDT, USDT/GBP, XEM/USD, XLM/ETH, XRP/ETH, DASH/USDT, DASH/ETH, XTZ/USD, DAI/USD, ADA/USD, DOT/EUR, BAT/USD, BCH/USDC, BSV/USD, BTC/GBP, DASH/BTC, LTC/PLN, USDT/USD, XLM/BTC, XRP/PLN, ZRX/PLN, QTUM/USDT, ADA/USDC, USDT/USDC, QTUM/USD, MKR/USD, SOL/USD, ATOM/ETH, ATOM/USDT, QASH/USD, VRA/USD, BCH/ETH, BSV/PLN, BTC/USD, ETH/BTC, LTC/BTC, OMG/USD, USDC/EUR, USDC/USD, USDC/USDT, XEM/BTC, XLM/EUR, XLM/USD, XRP/EUR, BSV/ETH, XLM/USDT, ZEC/USDT, BAT/USDC, LINK/USDC, SOL/BTC, DOGE/USD, DOGE/BTC, BAT/BTC, BAT/PLN, BCH/GBP, BCH/PLN, BCH/USD, BTC/USDC, ETH/USDC, OMG/BTC, BTC-PERPETUAL, ETH-PERPETUAL, ZRX/EUR, ADA/BTC, QTUM/ETH, DOT/USD, SOL/ETH, ATOM/BTC, ETH/USDT, EUR/PLN, LINK/PLN, LINK/USDT, OMG/ETH, XRP/BTC, XRP/USDT, ZEC/EUR, ADA/EUR, ADA/PLN, DOT/PLN, OMG/USDT, EUR/USDT, DOGE/USDT, GALA/USDT, BAT/ETH, BCH/EUR, BCH/USDT, BSV/BTC, DASH/USD, ETH/EUR, ETH/PLN, ETH/USD, GBP/USD, USD/PLN, XLM/PLN, XRP/GBP, ZIL/USD, USDT/PLN, XRP/USDC, QTUM/BTC, ADA/ETH, ZIL/BTC, SOL/USDT, LUNA/USDT, ATOM/USD</code>
            </td>
            <td>Provides streaming services an order book for selected symbol, user needs to provide levels of order book to receive. MAX is 20. MIN is 1. Order books are sorted based on NBBO price: BIDs best (Max) first then descending, ASKs best (MIN) first then ascending. The whole Order books is updated every 20MS regardless of changes.</td>
            <td>
                <code class="highlighter-rouge">
                {
                    "command": "SUBSCRIBE",
                    "event": "UPDATE",
                    "channel": "ORDER_BOOK_PUBLIC",
                    "data": [
                        {
                            "class": "OrderBook",
                            "exchange": "CROSSTOWER",
                            "symbol": "BTC/USD",
                            "bids": [
                                [
                                    19292.21,
                                    0.0124
                                ],
                                [
                                    19242.45,
                                    3.0516
                                ],
                                [
                                    10000.0,
                                    0.0002
                                ]
                                ],
                                "asks": [
                                [
                                    85100.0,
                                    0.01009
                                ],
                                [
                                    19397.85,
                                    21.6067
                                ],
                                [
                                    84300.0,
                                    0.00854
                                ]
                            ],
                            "eventTime": 1664651366635
                        },
                        ...
                    ]
                }
                </code>
            </td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">unsubscribe_order_books(instruments)</code></td>
            <td>**instruments:** list of pair of currencies.</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">trade_book_public(instruments)</code></td>
            <td>**instruments:** list of pair of currencies.</td>
            <td>Provides streaming services a trading book (public trades) for selected symbol. Once subscribed updates will be pushed to user as they appear at FlexFills.</td>
            <td><code class="highlighter-rouge">
            {
                "command": "SUBSCRIBE",
                "event": "UPDATE",
                "channel": "TRADE_PUBLIC",
                "data": [
                    {
                        "class": "PublicTrade",
                        "exchange": "OKCOIN",
                        "symbol": "BTC/USD",
                        "price": 19308.6,
                        "quantity": 0.0103,
                        "tradeSide": "BUY",
                        "eventTime": 1664651920827
                    },
                ...
                ]
            }
            </code></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">get_balance(currencies)</code></td>
            <td>**currencies:** list of selected currencies.</td>
            <td></td>
            <td><code class="highlighter-rouge">
            {
                "command": "SUBSCRIBE",
                "event": "SNAPSHOT",
                "channel": "BALANCE",
                "data": [
                    {
                    "class": "Balance",
                    "currencyCode": "ADA",
                    "balance": 16140.3555,
                    "available": 16040.3555,
                    "locked": 100.0
                    },
                    ...
                ]
            }
            </code></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">get_private_trades(instruments)</code></td>
            <td>**instruments:** list of pair of currencies.</td>
            <td>Private trades subscription will provide a snapshot of currently open ACTIVE orders and then updates via WebSocket.</td>
            <td><code class="highlighter-rouge">
            {
                "command": "GET",
                "event": "GET",
                "channel": "TRADE_PRIVATE",
                "data": [
                    {
                        "class": "Order",
                        "orderId": "567567567",
                        "exchOrderId": "1668662119644",
                        "direction": "BUY",
                        "orderType": "LIMIT",
                        "orderStatus": "ACTIVE",
                        "price": 12000.0,
                        "filledPrice": 0.0,
                        "amount": 0.001,
                        "orderDateTime": "2022-11-09T18:19:29.644164Z",
                        "globalInstrumentCd": "BTC/USD",
                        "message": null
                    }
                ]
            }
            </code></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">get_open_orders_list(order_data, instruments)</code></td>
            <td>
                <p>**order_data:** The dict of order data, including globalInstrumentCd, clientOrderId, exchangeOrderId</p>
                <p>* globalInstrumentCd - list of currencies pair. string</p>
                <p>* clientOrderId - Id of the order. string</p>
                <p>* exchangeOrderId - exchangeOrderId. string</p>
                <p>**instruments:** list of pair of currencies.</p>
            </td>
            <td>Get current list of open orders. One time request/response.</td>
            <td><code class="highlighter-rouge">
            {
                "command": "GET",
                "channel": "TRADE_PRIVATE",
                "data": [
                    {
                        "class": "Order",
                        "orderId": "567567567",
                        "exchOrderId": "1668662119644",
                        "direction": "BUY",
                        "orderType": "LIMIT",
                        "orderStatus": "ACTIVE",
                        "price": 12000.0,
                        "filledPrice": 0.0,
                        "amount": 0.001,
                        "orderDateTime": "2022-11-09T18:19:29.644164Z",
                        "globalInstrumentCd": "BTC/USD",
                        "message": null
                    }
                ]
            }
            </code></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">create_order(order_data)</code></td>
            <td>
                <p>**order_data:** The dict of order data, including globalInstrumentCd, clientOrderId, orderType, timeInForce, price, amount</p>
                <p>* globalInstrumentCd: list of currencies pair. string</p>
                <p>* clientOrderId: Id of the order. string</p>
                <p>* orderType: **market** - Market order, **limit** - Limit order. string</p>
                <p>* timeInForce: string, optional, **GTC** - Good till cancelled (default, orders are in order book for 90 days) **GTD** - Good till day, will terminate at end of day 4:59PM NY TIME **GTT** - Good till time, alive until specific date (cannot exceed 90 days) **FOK** - Fill or Kill, Fill full amount or nothing immediately **IOC** - Immediate or Cancel, Fill any amount and cancel the rest immediately</p>
                <p>* price: optional, Price only required for limit orders</p>
                <p>* amount: Quantity of the order</p>
            </td>
            <td>Get current list of open orders. One time request/response.</td>
            <td><code class="highlighter-rouge">
            {
                "command": "GET",
                "channel": "TRADE_PRIVATE",
                "data": [
                    {
                        "class": "Order",
                        "orderId": "567567567",
                        "exchOrderId": "1668662119644",
                        "direction": "BUY",
                        "orderType": "LIMIT",
                        "orderStatus": "ACTIVE",
                        "price": 12000.0,
                        "filledPrice": 0.0,
                        "amount": 0.001,
                        "orderDateTime": "2022-11-09T18:19:29.644164Z",
                        "globalInstrumentCd": "BTC/USD",
                        "message": null
                    }
                ]
            }
            </code></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">cancel_order(order_data)</code></td>
            <td>
                <p>**order_data:** The dict of order data, including globalInstrumentCd, clientOrderId or exchangeOrderId</p>
                <p>* globalInstrumentCd: list of currencies pair. string</p>
                <p>* clientOrderId: Id of the order. string</p>
                <p>* exchangeOrderId: exchangeOrderId. string</p>
            </td>
            <td>User may cancel existing orders; client may cancel one order by either including orderId or exchangeOrderId if orderId is not known. Only one parameter is needed and will be accepted. If no orderId or transactionId are added in the message than, all orders for selected pair/s will be cancelled. Must be subscribed to valid pair in order to cancel order in proper pair!</td>
            <td><code class="highlighter-rouge">
            {
                "command": "SUBSCRIBE",
                "event": "UPDATE",
                "channel": "TRADE_PRIVATE",
                "data": [
                    {
                        "class": "OrderUpdate",
                        "clientId": 100141,
                        "requestType": "SMART",
                        "tradeSide": "BUY",
                        "instrumentCd": "BTC/USD",
                        "exchangeOrderId": null,
                        "clientOrderId": null,
                        "transactionId": 1668897424879,
                        "orderRequestStatus": "CANCELLED",
                        "message": "",
                        "key": "100141:BTC/USD:352908720"
                    }
                ]
            }
            </code></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">modify_order(order_data)</code></td>
            <td>
                <p>**order_data:** The dict of order data, including globalInstrumentCd, clientOrderId or exchangeOrderId</p>
                <p>* globalInstrumentCd: list of currencies pair. string</p>
                <p>* clientOrderId: Id of the order. string</p>
                <p>* exchangeOrderId: exchangeOrderId. string</p>
                <p>* price: Price only required for limit orders</p>
                <p>* amount: Quantity of the order</p>
            </td>
            <td>Clients may update existing orders. Amount or Price can be modified. Client must use clientOrderId or exchangeOrderId Only one parameter is needed and will be accepted</td>
            <td><code class="highlighter-rouge">
            {
                "command": "GET",
                "event": "GET",
                "channel": "TRADE_PRIVATE",
                "data": [
                    {
                        "class": "Order",
                        "clientOrderId": "4444444",
                        "exchangeOrderId": "1668553243505",
                        "direction": "BUY",
                        "orderType": "LIMIT",
                        "orderStatus": "CANCELLED",
                        "price": 12700.0,
                        "filledPrice": 12700.0,
                        "amount": 0.001,
                        "orderDateTime": "2022-11-10T02:36:52.505443Z",
                        "globalInstrumentCd": "BTC/USD",
                        "message": null
                    },
                    ...
                ]
            }
            </code></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">get_trade_history(date_from, date_to, instruments)</code></td>
            <td>
                <p>**date_from:** Start date of required time frame, string. example: "2022-12-01T00:00:00"</p>
                <p>**date_to:** End date of required time frame, string. example: "2022-12-31T00:00:00"</p>
                <p>**instruments:** list of pair of currencies.</p>
            </td>
            <td>Clients may request a list **PARTIALLY_FILLED**, **FILLED** trades for a required time frame. Channel arguments ‘date-from’, ‘date-to’ are optional. If ‘date-from’ is not provided, it will be defaulted to ‘now minus 24 hours’. If ‘date-to’ is not provided, it will be defaulted to ‘now’.</td>
            <td><code class="highlighter-rouge">
            {
                "command": "GET",
                "event": "GET",
                "channel": "TRADE_PRIVATE",
                "data": [
                    {
                        "class": "Order",
                        "clientOrderId": "4444444",
                        "exchangeOrderId": "1668553243505",
                        "direction": "BUY",
                        "orderType": "LIMIT",
                        "orderStatus": "CANCELLED",
                        "price": 12700.0,
                        "filledPrice": 12700.0,
                        "amount": 0.001,
                        "orderDateTime": "2022-11-10T02:36:52.505443Z",
                        "globalInstrumentCd": "BTC/USD",
                        "message": null
                    },
                    ...
                ]
            }
            </code></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">get_order_history(date_from, date_to, instruments, statues)</code></td>
            <td>
                <p>**date_from:** Start date of required time frame, string. example: "2022-12-01T00:00:00"</p>
                <p>**date_to:** End date of required time frame, string. example: "2022-12-31T00:00:00"</p>
                <p>**instruments:** list of pair of currencies.</p>
                <p>**statues:** list of status.</p>
            </td>
            <td>Clients may request a list of **COMLETED**, **REJECTED**, **PARTIALLY_FILLED**, **FILLED**, **EXPIRED** order requests for a required time frame. Channel arguments ‘date-from’, ‘date-to’, ‘status’ are optional. If ‘date-from’ is not provided, it will be defaulted to ‘now minus 24 hours’. If ‘date-to’ is not provided, it will be defaulted to ‘now’. If ‘status‘ is not provided then trades with any status will be selected.</td>
            <td><code class="highlighter-rouge">
            {
               "command": "GET",
                "event": "GET",
                "channel": "TRADE_PRIVATE",
                "data": [
                    {
                        "class": "Order",
                        "clientOrderId": "4444444",
                        "exchangeOrderId": "1668553243505",
                        "direction": "BUY",
                        "orderType": "LIMIT",
                        "orderStatus": "CANCELLED",
                        "price": 12700.0,
                        "filledPrice": 12700.0,
                        "amount": 0.001,
                        "orderDateTime": "2022-11-10T02:36:52.505443Z",
                        "globalInstrumentCd": "BTC/USD",
                        "message": null
                    },
                    ...
                ]
            }
            </code></td>
        </tr>
        <tr>
            <td><code class="highlighter-rouge">get_trade_positions()</code></td>
            <td></td>
            <td></td>
            <td><code class="highlighter-rouge">
            {
                "command": "GET",
                "event": "GET",
                "channel": "TRADE_POSITIONS",
                "data": [
                    {
                        "class": "TradePosition",
                        "direction": "BUY",
                        "date": "2022-11-10",
                        "globalInstrumentCd": "BTC/USD",
                        "openPrice": 12700.0,
                        "entryPrice": 12700.0,
                        "posVolume": 0.001,
                        "currentSl": 10.0,
                        "currentTp": 10.0
                    },
                    ...
                ]
            }
            </code></td>
        </tr>
    </tbody>
</table>

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)
