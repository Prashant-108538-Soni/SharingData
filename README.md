import 'package:flutter/material.dart';
import 'package:hdfc_flutter_widgets/common/secondary_button.dart';
import 'package:hdfc_flutter_widgets/common/tertiary_button.dart';
import 'package:hdfc_flutter_widgets/event_card/common/bill_payment_status.dart';
import 'package:hdfc_flutter_widgets/event_card/common/biller_image.dart';
import 'package:hdfc_flutter_widgets/event_card/common/event_execution_pill.dart';
import 'package:hdfc_flutter_widgets/event_card/common/primary_detail.dart';
import 'package:hdfc_flutter_widgets/event_card/common/smart_pay_status.dart';

/// A compact card to display event details like bill payment status,
/// scheduled date, and smart pay status in a responsive layout.
class CompactEventCard extends StatelessWidget {
  // Required parameters for the event card.
  final List<String> menuOptions;
  final String eventIconPath;
  final String billerImagePath;
  final String smartPayStatus;
  final double amount;
  final String scheduledDate;
  final VoidCallback onTap;
  final ValueChanged<String> onSelect;
  final String smartPayIconPath;

  // Primary details
  final String eventName;
  final Color backgroundColor;
  final String accountDetails;
  final String billType;

  const CompactEventCard({
    Key? key,
    required this.menuOptions,
    required this.onTap,
    required this.onSelect,
    required this.eventIconPath,
    required this.billerImagePath,
    required this.smartPayStatus,
    required this.amount,
    required this.scheduledDate,
    required this.eventName,
    required this.backgroundColor,
    required this.accountDetails,
    required this.billType,
    required this.smartPayIconPath,
  }) : super(key: key);

  /// Common top container decoration
  BoxDecoration _topContainerDecoration(BuildContext context) => BoxDecoration(
        color: Colors.lightBlue[50],
        border: Border.all(
          color: Theme.of(context).primaryColor,
          width: 1.0,
        ),
        borderRadius: const BorderRadius.only(
          topLeft: Radius.circular(20),
          topRight: Radius.circular(20),
        ),
      );

  /// Common bottom container decoration
  BoxDecoration _bottomContainerDecoration(BuildContext context) => BoxDecoration(
        color: Colors.white,
        borderRadius: const BorderRadius.only(
          bottomLeft: Radius.circular(8),
          bottomRight: Radius.circular(8),
        ),
        border: Border(
          left: BorderSide(color: Theme.of(context).primaryColor, width: 1),
          right: BorderSide(color: Theme.of(context).primaryColor, width: 1),
          bottom: BorderSide(color: Theme.of(context).primaryColor, width: 1),
        ),
      );

  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(
      builder: (context, constraints) {
        return Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // Top section with event details and icons
            Container(
              decoration: _topContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 0),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  /// Header Row: Primary details and biller image
                  Row(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    children: [
                      // Event details
                      Expanded(
                        child: PrimaryDetail(
                          eventName: eventName,
                          svgPath: eventIconPath,
                          backgroundColor: backgroundColor,
                          accountDetails: accountDetails,
                          billType: billType,
                        ),
                      ),
                      // Biller logo
                      BillerImage(svgPath: billerImagePath, size: 50),
                    ],
                  ),
                  const SizedBox(height: 10),

                  /// SmartPay status
                  Padding(
                    padding: const EdgeInsets.symmetric(horizontal: 20),
                    child: SmartPayStatus(
                      svgPath: smartPayIconPath,
                      text: smartPayStatus,
                    ),
                  ),
                  const SizedBox(height: 20),
                ],
              ),
            ),

            // Bottom section with amount, date pill, and actions
            Container(
              decoration: _bottomContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 10),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  /// Row with amount + payment status and scheduled date
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      // Amount and bill status
                      Expanded(
                        child: Row(
                          mainAxisSize: MainAxisSize.min,
                          children: [
                            Flexible(
                              child: Text(
                                '₹ ${amount.toStringAsFixed(2)}',
                                style: const TextStyle(
                                  fontSize: 15,
                                  fontWeight: FontWeight.bold,
                                ),
                                overflow: TextOverflow.ellipsis,
                                maxLines: 1,
                              ),
                            ),
                            const SizedBox(width: 10),
                            Flexible(
                              child: BillPaymentStatus(
                                status: "Paid",
                                borderTextColor: Colors.red,
                                backgroundColor: Colors.red.shade50,
                              ),
                            ),
                          ],
                        ),
                      ),

                      // Scheduled date pill
                      EventExecutionPill(
                        eventDate: scheduledDate,
                        eventString: 'SCHEDULED',
                      ),
                    ],
                  ),

                  const SizedBox(height: 10),

                  /// Row with action button and menu
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      Expanded(
                        child: SecondaryButton(
                          title: "View Details",
                          onTap: onTap,
                        ),
                      ),
                      const SizedBox(width: 10),
                      TertiaryButton(
                        options: menuOptions,
                        onSelect: onSelect,
                        icon: const Icon(Icons.more_vert),
                      ),
                    ],
                  ),
                ],
              ),
            ),
          ],
        );
      },
    );
  }
}