

  	 Widget _openCallingDialog(var data) {
    var json = jsonDecode(data);
    var clientData = json['client_details'];
    var promoCode = json['promo_code'];
    assetsAudioPlayer.play();
    showGeneralDialog(
        barrierLabel:
            MaterialLocalizations.of(context).modalBarrierDismissLabel,
        barrierDismissible: true,
        barrierColor: Colors.black.withOpacity(0.6),
        transitionDuration: Duration(milliseconds: 700),
        context: context,
        pageBuilder: (_, __, ___) {
          return Material(
            type: MaterialType.transparency,
            child: Align(
              alignment: Alignment.center,
              child: Container(
                height: 480,
                margin: EdgeInsets.only(bottom: 12, left: 15, right: 15),
                decoration: BoxDecoration(
                  color: Colors.white,
                  borderRadius: BorderRadius.circular(12),
                ),
                child: Column(
                  children: [
                    Container(
                      height: 80,
                      alignment: Alignment.topCenter,
                      margin: EdgeInsets.only(top: 20, left: 30, right: 30),
                      child: Stack(
                        alignment: Alignment.topCenter,
                        children: [
                          Image.asset(
                            "assets/images/angular_shape_2.png",
                            width: MediaQuery.of(context).size.width,
                            height: 80,
                            fit: BoxFit.fitWidth,
                          ),
                          Padding(
                            padding: const EdgeInsets.only(top: 12),
                            child: Column(
                              mainAxisAlignment: MainAxisAlignment.start,
                              crossAxisAlignment: CrossAxisAlignment.center,
                              children: [
                                Text(
                                  "Calling for...",
                                  style: TextStyle(
                                      fontSize: 12, color: Colors.black),
                                ),
                                Text("Photography",
                                    style: TextStyle(
                                        fontSize: 17,
                                        color: AppTheme.primaryColor)),
                              ],
                            ),
                          ),
                        ],
                      ),
                    ),
                    Container(
                      margin: EdgeInsets.only(top: 30),
                      child: CircleAvatar(
                        radius: 100,
                        backgroundColor: Colors.black54,
                        child: CircleAvatar(
                          radius: 90,
                          backgroundColor: Colors.grey,
                          child: CircleAvatar(
                            radius: 80,
                            backgroundColor: Colors.white60,
                            backgroundImage: AssetImage("assets/images/logo_round.png"),
                          ),
                        ),
                      ),
                    ),

                    //**call controll button**//
                    Container(
                      margin: EdgeInsets.only(top: 40, left: 40, right: 40),
                      child: Row(
                        children: [
                          //accept button
                          InkWell(
                            onTap: () {
                              setState(() {
                                /*var photograher_lat =
                                    _currentLocation.latitude.toString();
                                var photograher_long =
                                    _currentLocation.latitude.toString();
                                //photographer clicked for call receive
                                socket.emit("callAccepted", [
                                  this.widget.user.token,
                                  //callingData.clientToken,
                                  photograher_lat,
                                  photograher_long
                                ]);*/
                                Navigator.pop(context);
                                assetsAudioPlayer.stop();
                                goToAccept(clientData);
                              });
                            },
                            child: CircleAvatar(
                              radius: 30,
                              backgroundColor: Colors.green,
                              child: Icon(
                                Icons.call,
                                color: Colors.white,
                                size: 26,
                              ),
                            ),
                          ),
                          Flexible(fit: FlexFit.tight, child: SizedBox()),

                          //reject button
                          InkWell(
                            onTap: () {
                              /*socket.emit("callToPhotographer", [
                                callingData.clientToken,
                                callingData.lat,
                                callingData.long
                              ]);
                              */
                              Navigator.pop(context);
                              assetsAudioPlayer.stop();
                            },
                            child: CircleAvatar(
                              radius: 30,
                              backgroundColor: Colors.red,
                              child: Icon(
                                Icons.call,
                                color: Colors.white,
                                size: 26,
                              ),
                            ),
                          )
                        ],
                      ),
                    )
                  ],
                ),
              ),
            ),
          );
        },
        transitionBuilder: (_, anim, __, child) {
          return SlideTransition(
            position:
                Tween(begin: Offset(0, 1), end: Offset(0, 0)).animate(anim),
            child: child,
          );
        });
  	}
