import 'package:flutter/material.dart';
import 'package:hdfc_flutter_widgets/common/secondary_button.dart';
import 'package:hdfc_flutter_widgets/common/tertiary_button.dart';
import 'package:hdfc_flutter_widgets/event_card/common/bill_payment_status.dart';
import 'package:hdfc_flutter_widgets/event_card/common/biller_image.dart';
import 'package:hdfc_flutter_widgets/event_card/common/event_execution_pill.dart';
import 'package:hdfc_flutter_widgets/event_card/common/primary_detail.dart';
import 'package:hdfc_flutter_widgets/event_card/common/smart_pay_status.dart';

/// A reusable and responsive compact event card widget.
/// Use this to show payment/event-related information in a summarized format.
class CompactEventCard extends StatelessWidget {
  /// List of menu options shown in the more options icon.
  final List<String> menuOptions;

  /// Callback when user taps 'View Details' button.
  final VoidCallback onTap;

  /// Callback when a menu option is selected.
  final ValueChanged<String> onSelect;

  /// Path to the event icon (usually an SVG).
  final String eventIconPath;

  /// Path to the biller logo/icon.
  final String billerImagePath;

  /// Label text for smart pay status (e.g. "Enabled", "Disabled").
  final String smartPayStatusText;

  /// Icon path for smart pay status.
  final String smartPayIconPath;

  /// Total amount to be paid/shown.
  final double amount;

  /// Status string for the bill (e.g. "Paid", "Overdue").
  final String billPaymentStatus;

  /// Bill status text background color.
  final Color billStatusBackgroundColor;

  /// Bill status text color.
  final Color billStatusTextColor;

  /// Scheduled event date string (e.g. "17 Sept").
  final String scheduledDate;

  /// Scheduled event label (e.g. "SCHEDULED", "PAID").
  final String scheduledLabel;

  /// Event name to display.
  final String eventName;

  /// Background color for event icon.
  final Color backgroundColor;

  /// User account or masked account string.
  final String accountDetails;

  /// Type of bill or service (e.g. "Electricity", "Mobile").
  final String billType;

  /// Text for "View Details" button.
  final String viewDetailsText;

  const CompactEventCard({
    Key? key,
    required this.menuOptions,
    required this.onTap,
    required this.onSelect,
    required this.eventIconPath,
    required this.billerImagePath,
    required this.smartPayStatusText,
    required this.smartPayIconPath,
    required this.amount,
    required this.billPaymentStatus,
    required this.billStatusBackgroundColor,
    required this.billStatusTextColor,
    required this.scheduledDate,
    required this.scheduledLabel,
    required this.eventName,
    required this.backgroundColor,
    required this.accountDetails,
    required this.billType,
    this.viewDetailsText = "View Details",
  }) : super(key: key);

  /// Top container decoration
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

  /// Bottom container decoration
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
            // Top section: Event details and smart pay
            Container(
              decoration: _topContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 0),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  // Event details + Biller logo
                  Row(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    children: [
                      Expanded(
                        child: PrimaryDetail(
                          eventName: eventName,
                          svgPath: eventIconPath,
                          backgroundColor: backgroundColor,
                          accountDetails: accountDetails,
                          billType: billType,
                        ),
                      ),
                      BillerImage(svgPath: billerImagePath, size: 50),
                    ],
                  ),
                  const SizedBox(height: 10),

                  // Smart Pay Status
                  Padding(
                    padding: const EdgeInsets.symmetric(horizontal: 20),
                    child: SmartPayStatus(
                      svgPath: smartPayIconPath,
                      text: smartPayStatusText,
                    ),
                  ),
                  const SizedBox(height: 20),
                ],
              ),
            ),

            // Bottom section: Payment info + actions
            Container(
              decoration: _bottomContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 10),
              child: Column(
                children: [
                  // Amount + Bill status + Date pill
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
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
                                status: billPaymentStatus,
                                borderTextColor: billStatusTextColor,
                                backgroundColor: billStatusBackgroundColor,
                              ),
                            ),
                          ],
                        ),
                      ),
                      EventExecutionPill(
                        eventDate: scheduledDate,
                        eventString: scheduledLabel,
                      ),
                    ],
                  ),
                  const SizedBox(height: 10),

                  // Bottom actions
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      Expanded(
                        child: SecondaryButton(
                          title: viewDetailsText,
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




CompactEventCard(
  menuOptions: ["Edit", "Delete"],
  onTap: () => print("View Details tapped"),
  onSelect: (option) => print("Selected: $option"),
  eventIconPath: 'assets/icons/mobile.svg',
  billerImagePath: 'assets/icons/jio.svg',
  smartPayStatusText: "Enabled",
  smartPayIconPath: 'assets/icons/auto_debit.svg',
  amount: 459.00,
  billPaymentStatus: "Paid",
  billStatusTextColor: Colors.red,
  billStatusBackgroundColor: Colors.red.shade50,
  scheduledDate: "17 Sept",
  scheduledLabel: "SCHEDULED",
  eventName: "Mobile Recharge",
  backgroundColor: Colors.blue,
  accountDetails: "XXXX 9089",
  billType: "Postpaid",
)